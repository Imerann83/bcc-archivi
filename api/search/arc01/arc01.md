# Ricerca "arc01"
Prima query di ricerca guidata.

## Interfaccia
Nel paragrafo sono descritti i filtri di ricerca e i risultati restituiti in termini di faccette e documenti a livello di interfaccia utente.

### Filtri impostabili
| Filtro | Tipo | Mandatorio / Facoltativo | Lista Valori - Descrizioni | Default |
|-|-|-|-|-|
| Cerca | Testo libero | Facoltativo |  |  |
| Entità di riferimento | Lista chiusa | Mandatorio | CA - Complesso archivistico, SC - Soggetto conservatore, SP - Soggetto produttore | Tutti i valori selezionati	|
| Provincia | Lista chiusa | Facoltativo | AV - Avellino, BN - Benevento, CA - Caserta, NA - Napoli, SA - Salerno | |
| Periodo Da | Lista chiusa | Facoltativo | 900, 1000, 1100, 1200, 1300, 1400, 1500, 1600, 1700, 1800, 1900, 2000 | | 
| Periodo A | Lista chiusa | Facoltativo | 900, 1000, 1100, 1200, 1300, 1400, 1500, 1600, 1700, 1800, 1900, 2000 | |

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
                        {{#ca.dates}}
                        {
                            "range": {
                                "dates": {
                                    "format": "yyyy-MM-dd",
                                    "relation": "intersects",
                                    {{#ca.dates.datefrom}}
                                    "gte": "{{ca.dates.datefrom}}"
                                    {{#ca.dates.dateto}},{{/ca.dates.dateto}}
                                    {{/ca.dates.datefrom}}
                                    {{#ca.dates.dateto}}
                                    "lte": "{{ca.dates.dateto}}"
                                    {{/ca.dates.dateto}}
                                }
                            }
                        }
                        {{#ca.place}},{{/ca.place}}
                        {{/ca.dates}}
                        {{#ca.place}}
                        {
                            "nested": {
                                "path": "sc",
                                "query": {
                                    "terms": {
                                        "sc.province": {{#toJson}}ca.place.province{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{/ca.place}}
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
                    ]
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
                        {{#sp.dates}}
                        {
                            "nested": {
                                "path": "sp",
                                "query": {
                                    "range": {
                                        "sp.dates": {
                                            "format": "yyyy-MM-dd",
                                            "relation": "intersects",
                                            {{#sp.dates.datefrom}}
                                            "gte": "{{sp.dates.datefrom}}"
                                            {{#sp.dates.dateto}},{{/sp.dates.dateto}}
                                            {{/sp.dates.datefrom}}
                                            {{#sp.dates.dateto}}
                                            "lte": "{{sp.dates.dateto}}"
                                            {{/sp.dates.dateto}}
                                        }
                                    }
                                }
                            }
                        }
                        {{#sp.place}},{{/sp.place}}
                        {{/sp.dates}}
                        {{#sp.place}}
                        {
                            "nested": {
                                "path": "sc",
                                "query": {
                                    "terms": {
                                        "sc.province": {{#toJson}}sp.place.province{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{/sp.place}}
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
                    ]
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
                        {{#sc.dates}}
                        {
                            "range": {
                                "dates": {
                                    "format": "yyyy-MM-dd",
                                    "relation": "intersects",
                                    {{#sc.dates.datefrom}}
                                    "gte": "{{sc.dates.datefrom}}"
                                    {{#sc.dates.dateto}},{{/sc.dates.dateto}}
                                    {{/sc.dates.datefrom}}
                                    {{#sc.dates.dateto}}
                                    "lte": "{{sc.dates.dateto}}"
                                    {{/sc.dates.dateto}}
                                }
                            }
                        }
                        {{#sc.place}},{{/sc.place}}
                        {{/sc.dates}}
                        {{#sc.place}}
                        {
                            "nested": {
                                "path": "sc",
                                "query": {
                                    "terms": {
                                        "sc.province": {{#toJson}}sc.place.province{{/toJson}}
                                    }
                                }
                            }
                        }
                        {{/sc.place}}
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
                    ]
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
| $.id | Mandatorio | Stringa | Identificativo del template di ricerca | Costante pari a "arc01" |
| $.params | Mandatorio | Oggetto | Contenitore dei parametri | |
| $.params.ca | Facoltativo\* | Oggetto | Contenitore dei parametri di ricerca per le entità  di tipo "Complesso archivistico". | Da inserire solo se selezionato il valore "CA" nel filtro "Entità di riferimento". |
| $.params.ca.query | Facoltativo | Stringa | Stringa di ricerca. | Da inserire solo se valorizzato il filtro "Cerca". |
| $.params.ca.province | Facoltativo | Vettore di stringhe. | Vettore costituito dalle province selezionate | Da inserire solo se risultano selezionati uno o più valori del filtro "Provincia". |
| $.params.ca.dates | Facoltativo | Oggetto | Contenitore dei parametri che delimitano il periodo di interesse. | Da inserire solo se risulta selezionato un valore per almeno uno dei filtri "Periodo Da" e "Periodo A". |
| $.params.ca.dates.datefrom | Facoltativo | Stringa formattata | Data di inizio del periodo di interesse. | Da inserire solo se risulta selezionato un valore per il filtro "Periodo Da". Al valore selezionato va concatenato il suffisso "-01-01" in modo da formare una data valida nel formato "yyyy-MM-dd". |
| $.params.ca.dates.dateto | Facoltativo | Stringa formattata | Data di fine del periodo di interesse. | Da inserire solo se risulta selezionato un valore per il filtro "Periodo A". Al valore selezionato va concatenato il suffisso "-12-31" in modo da formare una data valida nel formato "yyyy-MM-dd". |
| $.params.sc | Facoltativo\* | Oggetto | Contenitore dei parametri di ricerca per le entità  di tipo "Soggetto conservatore" | Da inserire solo se selezionato il valore "SC" nel filtro "Entità di riferimento" |
| $.params.sc.query | Facoltativo | Stringa | Stringa di ricerca. | Da inserire solo se valorizzato il filtro "Cerca". |
| $.params.sc.province | Facoltativo | Vettore di stringhe. | Vettore costituito dalle province selezionate | Da inserire solo se risultano selezionati uno o più valori del filtro "Provincia". |
| $.params.sc.dates | Facoltativo | Oggetto | Contenitore dei parametri che delimitano il periodo di interesse. | Da inserire solo se risulta selezionato un valore per almeno uno dei filtri "Periodo Da" e "Periodo A". |
| $.params.sc.dates.datefrom | Facoltativo | Stringa formattata | Data di inizio del periodo di interesse. | Da inserire solo se risulta selezionato un valore per il filtro "Periodo Da". Al valore selezionato va concatenato il suffisso "-01-01" in modo da formare una data valida nel formato "yyyy-MM-dd". |
| $.params.sc.dates.dateto | Facoltativo | Stringa formattata | Data di fine del periodo di interesse. | Da inserire solo se risulta selezionato un valore per il filtro "Periodo A". Al valore selezionato va concatenato il suffisso "-12-31" in modo da formare una data valida nel formato "yyyy-MM-dd". |
| $.params.sp | Facoltativo\* | Oggetto | Contenitore dei parametri di ricerca per le entità  di tipo "Soggetto produttore" | Da inserire solo se selezionato il valore "SP" nel filtro "Entità di riferimento" |
| $.params.sp.query | Facoltativo | Stringa | Stringa di ricerca. | Da inserire solo se valorizzato il filtro "Cerca". |
| $.params.sp.province | Facoltativo | Vettore di stringhe. | Vettore costituito dalle province selezionate | Da inserire solo se risultano selezionati uno o più valori del filtro "Provincia". |
| $.params.sp.dates | Facoltativo | Oggetto | Contenitore dei parametri che delimitano il periodo di interesse. | Da inserire solo se risulta selezionato un valore per almeno uno dei filtri "Periodo Da" e "Periodo A". |
| $.params.sp.dates.datefrom | Facoltativo | Stringa formattata | Data di inizio del periodo di interesse. | Da inserire solo se risulta selezionato un valore per il filtro "Periodo Da". Al valore selezionato va concatenato il suffisso "-01-01" in modo da formare una data valida nel formato "yyyy-MM-dd". |
| $.params.sp.dates.dateto | Facoltativo | Stringa formattata | Data di fine del periodo di interesse. | Da inserire solo se risulta selezionato un valore per il filtro "Periodo A". Al valore selezionato va concatenato il suffisso "-12-31" in modo da formare una data valida nel formato "yyyy-MM-dd". |

\*Almeno uno tra "$.params.ca", "$.params.sc" e "$.params.sp" deve essere presente.

Di seguito un body di esempio.

<details>
<summary>Espandi</summary>
<p>

```JSON
{
    "id": "arc01",
    "params": {
        "ca": {
            "query": "archivio complesso manoscritto sottoscritto Finsiel Almawave",
            "place": {
                "province": [
                    "RM",
                    "PG"
                ]
            },
            "dates": {
                "datefrom": "1900-01-01",
                "dateto": "2100-12-31"
            }
        },
        "sp": {
            "query": "archivio complesso manoscritto sottoscritto Finsiel Almawave",
            "place": {
                "province": [
                    "RM",
                    "PG"
                ]
            },
            "dates": {
                "datefrom": "1900-01-01",
                "dateto": "2100-12-31"
            }
        },
        "sc": {
            "query": "archivio complesso manoscritto sottoscritto Finsiel Almawave",
            "place": {
                "province": [
                    "RM",
                    "PG"
                ]
            },
            "dates": {
                "datefrom": "1900-01-01",
                "dateto": "2100-12-31"
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
    "took": 13,
    "timed_out": false,
    "_shards": {
        "total": 4,
        "successful": 4,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 9,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "sc": {
            "doc_count": 9,
            "sc_nested": {
                "doc_count": 9,
                "sc_count": {
                    "value": 2
                }
            }
        },
        "sp": {
            "doc_count": 9,
            "sp_nested": {
                "doc_count": 10,
                "sp_count": {
                    "value": 4
                }
            }
        },
        "ca": {
            "doc_count": 9,
            "ca_count": {
                "value": 3
            }
        }
    }
}
```

</p>
</details>
