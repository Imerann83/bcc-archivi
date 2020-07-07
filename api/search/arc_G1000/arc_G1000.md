# Ricerca "arc_G1000"
Prima query di ricerca guidata.

## Interfaccia
Nel paragrafo sono descritti i filtri di ricerca e i risultati restituiti in termini di faccette e documenti a livello di interfaccia utente.

### Filtri impostabili
| Filtro | Tipo | Mandatorio / Facoltativo | Lista Valori : Descrizioni | Default |
|-|-|-|-|-|
| Cerca | Testo libero | Facoltativo |  |  |
| Entità di riferimento | Lista chiusa | Mandatorio | ca : Complesso archivistico, sc : Soggetto conservatore, sp : Soggetto produttore | Tutti i valori selezionati	|
| Provincia | Lista chiusa | Facoltativo | AV : Avellino, BN : Benevento, CE : Caserta, NA : Napoli, SA : Salerno | |
| Periodo Da | Lista chiusa | Facoltativo | 0101-0200 : 100, 0201-0300 : 200, 0301-0400 : 300, 0401-0500 : 400, 0501-0600 : 500, 0601-0700 : 600, 0701-0800 : 700, 0801-0900 : 800, 0901-1000 : 900, 1001-1100 : 1000, 1101-1200 : 1100, 1201-1300 : 1200, 1301-1400 : 1300, 1401-1500 : 1400, 1501-1600 : 1500, 1601-1700 : 1600, 1701-1800 : 1700, 1801-1900 : 1800, 1901-2000 : 1900, 2001-2100 : 2000 | | 
| Periodo A | Lista chiusa | Facoltativo | 0101-0200 : 100, 0201-0300 : 200, 0301-0400 : 300, 0401-0500 : 400, 0501-0600 : 500, 0601-0700 : 600, 0701-0800 : 700, 0801-0900 : 800, 0901-1000 : 900, 1001-1100 : 1000, 1101-1200 : 1100, 1201-1300 : 1200, 1301-1400 : 1300, 1401-1500 : 1400, 1501-1600 : 1500, 1601-1700 : 1600, 1701-1800 : 1700, 1801-1900 : 1800, 1901-2000 : 1900, 2001-2100 : 2000 | |

### Faccette restituite
La pagina di interfaccia prevede la visualizzazione di una serie di faccette descritte nella tabella seguente. La faccetta va mostrata solo nel caso in cui il relativo valore risulti maggiore di zero.
| Faccetta | Descrizione | Chiave | Valore | Ordinamento | Dimensione base | Dimensione incremento |  
|-|-|-|-|-|-|-|
| Complessi Archivistici | Aggregazione per tipo entità "Complesso archivistico" | Costante pari a "Complessi archivistici" | Conteggio distinto dei Complessi archivistici radice contenenti altri Complessi archivistici o Unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati. | Valore decrescente | 1 | 0 |
| Soggetti Conservatori | Aggregazione per tipo entità "Soggetto conservatore" | Costante pari a "Soggetti conservatori" | Conteggio distinto dei Soggetti conservatori soddisfacenti i criteri di ricerca impostati. | Valore decrescente | 1 | 0 |
| Soggetti Produttori | Aggregazione per tipo entità "Soggetto produttore" | Costante pari a "Soggetti produttori" | Conteggio distinto dei Soggetti produttori soddisfacenti i criteri di ricerca impostati. | Valore decrescente | 1 | 0 | 

### Documenti restituiti
La pagina di interfaccia non prevede la visualizzazione di una lista di documenti in risposta alla ricerca effettuata.

## Elasticsearch template
Nel paragrafo è riportato il template di ricerca implementato in elasticsearch e richiamato dal servizio esposto. Il template è uno script in linguaggio "mustache" che compone dinamicamente la query elasticsearch in funzione dei parametri passati al momento della chiamata.

<details>
<summary>Espandi</summary>
<p>

```HTML+Django
{
    "size": 0,
    "aggs": {
        {{#ca}}
        "ca": {
            "filter": {
                "bool": {
                    "filter": [
                        {{#ca.century_from}}
                        {
                            "terms": {
                                "century_from": {{#toJson}}ca.century_from.centuries{{/toJson}}
                            }
                        }
                        {{#ca.century_to}},{{/ca.century_to}}
                        {{^ca.century_to}}{{#ca.province}},{{/ca.province}}{{/ca.century_to}}
                        {{/ca.century_from}}
                        {{#ca.century_to}}
                        {
                            "terms": {
                                "century_to": {{#toJson}}ca.century_to.centuries{{/toJson}}
                            }
                        }
                        {{#ca.province}},{{/ca.province}}
                        {{/ca.century_to}}
                        {{#ca.province}}
                        {
                            "nested": {
                                "path": "sc",
                                "query": {
                                    "terms": {
                                        "sc.province": {{#toJson}}ca.province.provinces{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{/ca.province}}
                    ],
                    "should": [
                        {{#ca.query}}
                        {
                            "multi_match": {
                                "query": "{{ca.query}}",
                                "type": "best_fields",
                                "fields": [
                                    "names",
                                    "content",
                                    "history",
                                    "description"
                                ]
                            }
                        },
                        {
                            "nested": {
                                "path": "uad",
                                "query": {
                                    "multi_match": {
                                        "query": "{{ca.query}}",
                                        "type": "best_fields",
                                        "fields": [
                                            "uad.names",
                                            "uad.content",
                                            "uad.history",
                                            "uad.description"
                                        ]
                                    }
                                }
                            }
                        }
                        {{/ca.query}}
                    ],
                    "minimum_should_match":{{#ca.query}}1{{/ca.query}}{{^ca.query}}0{{/ca.query}}
                }
            },
            "aggs": {
                "ca_count": {
                    "cardinality": {
                        "field": "root_uri"
                    }
                }
            }
        }
        {{#sp}},{{/sp}}
        {{^sp}}{{#sc}},{{/sc}}{{/sp}}
        {{/ca}}
        {{#sp}}
        "sp": {
            "filter": {
                "bool": {
                    "filter": [
                        {{#sp.century_from}}
                        {
                            "nested": {
                                "path": "sp",
                                "query": {
                                    "terms": {
                                        "sp.century_from": {{#toJson}}sp.century_from.centuries{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{#sp.century_to}},{{/sp.century_to}}
                        {{^sp.century_to}}{{#sp.province}},{{/sp.province}}{{/sp.century_to}}
                        {{/sp.century_from}}
                        {{#sp.century_to}}
                        {
                            "nested": {
                                "path": "sp",
                                "query": {
                                    "terms": {
                                        "sp.century_to": {{#toJson}}sp.century_to.centuries{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{#sp.province}},{{/sp.province}}
                        {{/sp.century_to}}
                        {{#sp.province}}
                        {
                            "nested": {
                                "path": "sc",
                                "query": {
                                    "terms": {
                                        "sc.province": {{#toJson}}sp.province.provinces{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{/sp.province}}
                    ],
                    "should": [
                        {{#sp.query}}
                        {
                            "nested": {
                                "path": "sp",
                                "query": {
                                    "multi_match": {
                                        "query": "{{sp.query}}",
                                        "type": "best_fields",
                                        "fields": [
                                            "sp.names",
                                            "sp.content",
                                            "sp.history",
                                            "sp.description"
                                        ]
                                    }
                                }
                            }
                        }
                        {{/sp.query}}
                    ],
                    "minimum_should_match":{{#sp.query}}1{{/sp.query}}{{^sp.query}}0{{/sp.query}}
                }
            },
            "aggs": {
                "sp_nested": {
                    "nested": {
                        "path": "sp"
                    },
                    "aggs": {
                        "sp_count": {
                            "cardinality": {
                                "field": "sp.uri"
                            }
                        }
                    }
                }
            }
        }
        {{#sc}},{{/sc}}
        {{/sp}}
        {{#sc}}
        "sc": {
            "filter": {
                "bool": {
                    "filter": [
                        {{#sc.century_from}}
                        {
                            "terms": {
                                "century_from": {{#toJson}}sc.century_from.centuries{{/toJson}}
                            }
                        }
                        {{#sc.century_to}},{{/sc.century_to}}
                        {{^sc.century_to}}{{#sc.province}},{{/sc.province}}{{/sc.century_to}}
                        {{/sc.century_from}}
                        {{#sc.century_to}}
                        {
                            "terms": {
                                "century_to": {{#toJson}}sc.century_to.centuries{{/toJson}}
                            }
                        }
                        {{#sc.province}},{{/sc.province}}
                        {{/sc.century_to}}
                        {{#sc.province}}
                        {
                            "nested": {
                                "path": "sc",
                                "query": {
                                    "terms": {
                                        "sc.province": {{#toJson}}sc.province.provinces{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{/sc.province}}
                    ],
                    "should": [
                        {{#sc.query}}
                        {
                            "nested": {
                                "path": "sc",
                                "query": {
                                    "multi_match": {
                                        "query": "{{sc.query}}",
                                        "type": "best_fields",
                                        "fields": [
                                            "sc.names",
                                            "sc.content",
                                            "sc.history",
                                            "sc.description"
                                        ]
                                    }
                                }
                            }
                        }
                        {{/sc.query}}
                    ],
                    "minimum_should_match":{{#sc.query}}1{{/sc.query}}{{^sc.query}}0{{/sc.query}}
                }
            },
            "aggs": {
                "sc_nested": {
                    "nested": {
                        "path": "sc"
                    },
                    "aggs": {
                        "sc_count": {
                            "cardinality": {
                                "field": "sc.uri"
                            }
                        }
                    }
                }
            }
        }
        {{/sc}}
    }
}
```

</p>
</details>

## Search API
Nel paragrafo sono descritte le modalità di interrogazione e di interpretazione delle risposte restituite dal servizio di ricerca esposto.

### Endpoint
Il servizio è richiamabile in basic authentication (admin/admin) con metodo GET al seguente indirizzo
https://10.121.172.70:9200/bcc-archivi/_search/template

### Richiesta 
La richiesta al servizio di ricerca esposto va inoltrata con un body in formato "JSON" descritto nella tabella seguente.
| Json Path | Mandatorio / Facoltativo | Tipo | Descrizione | Valore |
|-|-|-|-|-|
| $.id | Mandatorio | Stringa | Identificativo del template di ricerca | Costante pari a "arc_G1000" |
| $.params | Mandatorio | Oggetto | Contenitore dei parametri | |
| $.params.ca | Facoltativo\* | Oggetto | Contenitore dei parametri di ricerca per le entità  di tipo "Complesso archivistico". | Da inserire solo se selezionato il valore "CA" nel filtro "Entità di riferimento". |
| $.params.ca.query | Facoltativo | Stringa | Stringa di ricerca. | Da inserire solo se valorizzato il filtro "Cerca". |
| $.params.ca.province | Facoltativo | Oggetto | Contenitore dei parametri che identificano le province di interesse. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Provincia". |
| $.params.ca.province.provinces | Facoltativo | Vettore di stringhe. | Vettore costituito dalle province selezionate | Da inserire solo se risulta selezionato almeno un valore del filtro "Provincia". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.ca.century_from | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo a". |
| $.params.ca.century_from.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo da". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.ca.century_to | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo a". |
| $.params.ca.century_to.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo a". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.sc | Facoltativo\* | Oggetto | Contenitore dei parametri di ricerca per le entità  di tipo "Soggetto conservatore" | Da inserire solo se selezionato il valore "SC" nel filtro "Entità di riferimento" |
| $.params.sc.query | Facoltativo | Stringa | Stringa di ricerca. | Da inserire solo se valorizzato il filtro "Cerca". |
| $.params.sc.province | Facoltativo | Oggetto | Contenitore dei parametri che identificano le province di interesse. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Provincia". |
| $.params.sc.province.provinces | Facoltativo | Vettore di stringhe. | Vettore costituito dalle province selezionate | Da inserire solo se risulta selezionato almeno un valore del filtro "Provincia". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.sc.century_from | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo a". |
| $.params.sc.century_from.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo da". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.sc.century_to | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo a". |
| $.params.sc.century_to.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo a". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.sp | Facoltativo\* | Oggetto | Contenitore dei parametri di ricerca per le entità  di tipo "Soggetto produttore" | Da inserire solo se selezionato il valore "SP" nel filtro "Entità di riferimento" |
| $.params.sp.query | Facoltativo | Stringa | Stringa di ricerca. | Da inserire solo se valorizzato il filtro "Cerca". |
| $.params.sp.province | Facoltativo | Oggetto | Contenitore dei parametri che identificano le province di interesse. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Provincia". |
| $.params.sp.province.provinces | Facoltativo | Vettore di stringhe. | Vettore costituito dalle province selezionate | Da inserire solo se risulta selezionato almeno un valore del filtro "Provincia". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.sp.century_from | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo a". |
| $.params.sp.century_from.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo da". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.sp.century_to | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo a". |
| $.params.sp.century_to.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo a". Utilizzare le chiavi associate ai valori selezionati. |

\*Almeno uno tra "$.params.ca", "$.params.sc" e "$.params.sp" deve essere presente.

Di seguito un body di esempio.

<details>
<summary>Espandi</summary>
<p>

```JSON
{
    "id": "arc_G1000",
    "params": {
        "ca": {
            "query": "archivio complesso manoscritto sottoscritto Finsiel Almawave",
            "century_from": {
                "centuries": [
                    "1901-2000"
                ]
            },
            "century_to": {
                "centuries": [
                    "2001-2100",
                    "1901-2000"
                ]
            },
            "province": {
                "provinces": [
                    "NA",
                    "SA"
                ]
            }
        },
        "sp": {
            "query": "archivio complesso manoscritto sottoscritto Finsiel Almawave",
            "century_from": {
                "centuries": [
                    "1901-2000"
                ]
            },
            "century_to": {
                "centuries": [
                    "1901-2000"
                ]
            },
            "province": {
                "provinces": [
                    "NA",
                    "SA"
                ]
            }
        },
        "sc": {
            "query": "archivio complesso manoscritto sottoscritto Finsiel Almawave",
            "century_from": {
                "centuries": [
                    "1901-2000"
                ]
            },
            "century_to": {
                "centuries": [
                    "1901-2000"
                ]
            },
            "province": {
                "provinces": [
                    "NA",
                    "SA"
                ]
            }
        }
    }
}
```

</p>
</details>

### Risposta
La risposta restituita dal servizio di ricerca è descritta nella tabella seguente; sono riportati soltanto i path contenenti le informazioni necessarie alla visualizzazione dei dati in interfaccia.
| Json Path | Tipo | Descrizione | Valore | Faccetta |
|-|-|-|-|-|
| $.aggregations.ca.ca_count.value | Intero | Numero di entità di tipo "Complesso Archivistico" individuate in funzione dei criteri di ricerca inseriti. | Valorizzato solo se selezionato il valore "CA" nel filtro "Entità di riferimento". | Complessi archivistici |
| $.aggregations.sc.sc_nested.sc_count.value | Intero | Numero di entità di tipo "Soggetto conservatore" individuate in funzione dei criteri di ricerca inseriti. | Valorizzato solo se selezionato il valore "SC" nel filtro "Entità di riferimento". | Soggetti conservatori |
| $.aggregations.sp.sp_nested.sp_count.value | Intero | Numero di entità di tipo "Soggetto produttore" individuate in funzione dei criteri di ricerca inseriti. | Valorizzato solo se selezionato il valore "SP" nel filtro "Entità di riferimento". | Soggetti produttori |

Di seguito una risposta di esempio.

<details>
<summary>Espandi</summary>
<p>

```JSON
{
    "took": 26,
    "timed_out": false,
    "_shards": {
        "total": 4,
        "successful": 4,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 3331,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "sc": {
            "doc_count": 35,
            "sc_nested": {
                "doc_count": 35,
                "sc_count": {
                    "value": 4
                }
            }
        },
        "sp": {
            "doc_count": 5,
            "sp_nested": {
                "doc_count": 20,
                "sp_count": {
                    "value": 19
                }
            }
        },
        "ca": {
            "doc_count": 14,
            "ca_count": {
                "value": 14
            }
        }
    }
}
```

</p>
</details>
