# Ricerca "arc_G1100"
Prima query di ricerca guidata per Complesso archivistico.

## Interfaccia
Nel paragrafo sono descritti i filtri di ricerca e i risultati restituiti in termini di faccette e documenti a livello di interfaccia utente.

### Filtri impostabili
| Filtro | Tipo | Mandatorio / Facoltativo | Lista Valori : Descrizioni | Default |
|-|-|-|-|-|
| Cerca | Testo libero | Facoltativo |  |  |
| Provincia | Lista chiusa | Facoltativo | AV : Avellino, BN : Benevento, CE : Caserta, NA : Napoli, SA : Salerno | |
| Secolo Da | Lista chiusa | Facoltativo | 0101-0200, 0201-0300, 0301-0400, 0401-0500, 0501-0600, 0601-0700, 0701-0800, 0801-0900, 0901-1000, 1001-1100, 1101-1200, 1201-1300, 1301-1400, 1401-1500, 1501-1600, 1601-1700, 1701-1800, 1801-1900, 1901-2000, 2001-2100 | | 
| Venticinquennio Da | Lista chiusa | Facoltativo | 0101-0125, 0126-0150, 0151-0175, 0176-0200, 0201-0225, 0226-0250, 0251-0275, 0276-0300, 0301-0325, 0326-0350, 0351-0375, 0376-0400, 0401-0425, 0426-0450, 0451-0475, 0476-0500, 0501-0525, 0526-0550, 0551-0575, 0576-0600, 0601-0625, 0626-0650, 0651-0675, 0676-0700, 0701-0725, 0726-0750, 0751-0775, 0776-0800, 0801-0825, 0826-0850, 0851-0875, 0876-0900, 0901-0925, 0926-0950, 0951-0975, 0976-0900, 1001-1025, 1026-1050, 1051-1075, 1076-1100, 1101-1125, 1126-1150, 1151-1175, 1176-1200, 1201-1225, 1226-1250, 1251-1275, 1276-1300, 1301-1325, 1326-1350, 1351-1375, 1376-1400, 1401-1425, 1426-1450, 1451-1475, 1476-1500, 1501-1525, 1526-1550, 1551-1575, 1576-1600, 1601-1625, 1626-1650, 1651-1675, 1676-1700, 1701-1725, 1726-1750, 1751-1775, 1776-1800, 1801-1825, 1826-1850, 1851-1875, 1876-1900, 1901-1925, 1926-1950, 1951-1975, 1976-2000, 2001-2025, 2026-2050, 2051-2075, 2076-2100 | |
| Secolo A | Lista chiusa | Facoltativo | 0101-0200, 0201-0300, 0301-0400, 0401-0500, 0501-0600, 0601-0700, 0701-0800, 0801-0900, 0901-1000, 1001-1100, 1101-1200, 1201-1300, 1301-1400, 1401-1500, 1501-1600, 1601-1700, 1701-1800, 1801-1900, 1901-2000, 2001-2100 | | 
| Venticinquennio A | Lista chiusa | Facoltativo | 0101-0125, 0126-0150, 0151-0175, 0176-0200, 0201-0225, 0226-0250, 0251-0275, 0276-0300, 0301-0325, 0326-0350, 0351-0375, 0376-0400, 0401-0425, 0426-0450, 0451-0475, 0476-0500, 0501-0525, 0526-0550, 0551-0575, 0576-0600, 0601-0625, 0626-0650, 0651-0675, 0676-0700, 0701-0725, 0726-0750, 0751-0775, 0776-0800, 0801-0825, 0826-0850, 0851-0875, 0876-0900, 0901-0925, 0926-0950, 0951-0975, 0976-0900, 1001-1025, 1026-1050, 1051-1075, 1076-1100, 1101-1125, 1126-1150, 1151-1175, 1176-1200, 1201-1225, 1226-1250, 1251-1275, 1276-1300, 1301-1325, 1326-1350, 1351-1375, 1376-1400, 1401-1425, 1426-1450, 1451-1475, 1476-1500, 1501-1525, 1526-1550, 1551-1575, 1576-1600, 1601-1625, 1626-1650, 1651-1675, 1676-1700, 1701-1725, 1726-1750, 1751-1775, 1776-1800, 1801-1825, 1826-1850, 1851-1875, 1876-1900, 1901-1925, 1926-1950, 1951-1975, 1976-2000, 2001-2025, 2026-2050, 2051-2075, 2076-2100 | |
| Soggetto produttore | Lista chiusa | Facoltativo | Identificativi dei Soggetti produttori selezionabili da apposita faccetta | |
| Soggetto conservatore | Lista chiusa | Facoltativo | Identificativi dei Soggetti conservatori selezionabili da apposita faccetta | |

### Faccette restituite
La pagina di interfaccia prevede la visualizzazione di una serie di faccette descritte nella tabella seguente. La faccetta va mostrata solo nel caso in cui il relativo valore risulti maggiore di zero.
| Faccetta | Descrizione | Chiave | Valore | Ordinamento | Dimensione base | Dimensione incremento |  
|-|-|-|-|-|-|-|
| Provincia | Aggregazione dei complessi archivistici radice per Provincia | Denominazione Provincia | Conteggio distinto dei Complessi archivistici radice contenenti altri Complessi archivistici o Unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati. | Chiave crescente | 5 | 0 |
| Periodo A | Aggregazione dei complessi archivistici radice per Secolo - Venticinquennio dell'estremo remoto di esistenza | Secolo - Venticinquennio remoto | Conteggio distinto dei Complessi archivistici radice contenenti altri Complessi archivistici o Unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati. | Chiave crescente | 5 | 5 |
| Periodo Da | Aggregazione dei complessi archivistici radice per Secolo - Venticinquennio dell'estremo recente di esistenza | Secolo - Venticinquennio recente | Conteggio distinto dei Complessi archivistici radice contenenti altri Complessi archivistici o Unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati. | Chiave crescente | 5 | 5 |
| Soggetti Conservatori | Aggregazione dei complessi archivistici radice per Soggetto conservatore | Denominazione Soggetto conservatore | Conteggio distinto dei Complessi archivistici radice contenenti altri Complessi archivistici o Unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati. | Chiave crecente| 5 | 5 |
| Soggetti Produttori | Aggregazione dei complessi archivistici radice per Soggetto produttore | Denominazione Soggetto produttore | Conteggio distinto dei Complessi archivistici radice contenenti altri Complessi archivistici o Unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati. | Chiave crecente | 5 | 5 | 

### Documenti restituiti
La pagina di interfaccia prevede la visualizzazione della lista paginata di Complessi archivistici radice contenenti altri Complessi archivistici o Unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati.
Ognuno dei documenti restituiti è corredato dalla seguente di lista di attributi, eventualmente associati a metriche.
| Attributo | Descrizione | Mandatorio / Facoltativo | Cardinalità | Chiave | Valore |  
|-|-|-|-|-|-|
| Denominazione | Denominazione principale del Complesso archivistico radice | Mandatorio | Univoco | | |
| Tipo Complesso archivistico | Tipologia dei complessi archivistici contenuti nel Complesso archivistico radice che soddisfano i criteri di ricerca impostati| Facoltativo | Multivalore | Tipo Complesso Archivistico | Conteggio distinto dei complessi archivistici contenuti nel Complesso archivistico radice che soddisfano i criteri di ricerca impostati |
| Unità | Aggregazione per Unità archivistiche / documentarie contenute nel Complesso archivistico radice che soddisfano i criteri di ricerca impostati| Facoltativo | Univoco | Valore costante pari a "Unità" | Conteggio distinto delle Unità archivistiche / documentarie contenute nel Complesso archivistico radice che soddisfano i criteri di ricerca impostati |

## Elasticsearch template
Nel paragrafo è riportato il template di ricerca implementato in elasticsearch e richiamato dal servizio esposto. Il template è uno script in linguaggio "mustache" che compone dinamicamente la query elasticsearch in funzione dei parametri passati al momento della chiamata.

<details>
<summary>Espandi</summary>
<p>

```HTML+Django
{
    "size": 0,
    "query": {
        "bool": {
            "filter": [
                {{#ca.century_from}}
                        {
                    "terms": {
                        "century_from": {{#toJson}}ca.century_from.centuries{{/toJson}}
                    }
                }
                {{#ca.century_quarter_from}},
                {
                    "terms": {
                        "century_quarter_from": {{#toJson}}ca.century_quarter_from.quarters{{/toJson}}
                    }
                }
                {{/ca.century_quarter_from}}
                {{#ca.century_to}},{{/ca.century_to}}
                {{^ca.century_to}}{{#ca.province}},{{/ca.province}}{{/ca.century_to}}
                {{^ca.century_to}}{{^ca.province}}{{#ca.creator}},{{/ca.creator}}{{/ca.province}}{{/ca.century_to}}
                {{^ca.century_to}}{{^ca.province}}{{^ca.creator}}{{#ca.holder}},{{/ca.holder}}{{/ca.creator}}{{/ca.province}}{{/ca.century_to}}
                {{/ca.century_from}}
                {{#ca.century_to}}
                {
                    "terms": {
                        "century_to": {{#toJson}}ca.century_to.centuries{{/toJson}}
                    }
                }
                {{#ca.century_quarter_to}},
                {
                    "terms": {
                        "century_quarter_to": {{#toJson}}ca.century_quarter_to.quarters{{/toJson}}
                    }
                }
                {{/ca.century_quarter_to}}
                {{#ca.province}},{{/ca.province}}
                {{^ca.province}}{{#ca.creator}},{{/ca.creator}}{{/ca.province}}
                {{^ca.province}}{{^ca.creator}}{{#ca.holder}},{{/ca.holder}}{{/ca.creator}}{{/ca.province}}
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
                {{#ca.creator}},{{/ca.creator}}
                {{^ca.creator}}{{#ca.holder}},{{/ca.holder}}{{/ca.creator}}
                {{/ca.province}}
                {{#ca.creator}}
                {
                    "nested": {
                        "path": "sp",
                        "query": {
                            "terms": {
                                "sp.uri": {{#toJson}}ca.creator.creators{{/toJson}}
                            }
                        }
                    }
                }
                {{#ca.holder}},{{/ca.holder}}
                {{/ca.creator}}
                {{#ca.holder}}
                {
                    "nested": {
                        "path": "sc",
                        "query": {
                            "terms": {
                                "sc.uri": {{#toJson}}ca.holder.holders{{/toJson}}
                            }
                        }
                    }
                }
                {{/ca.holder}}
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
        },
        "sp_filter": {
            "nested": {
                "path": "sp"
            },
            "aggs": {
                "sp_count": {
                    "cardinality": {
                        "field": "sp.uri"
                    }
                },
                "sp_buckets": {
                    "composite": {
                        "size": {{ca.creator_size}}{{^ca.creator_size}}5{{/ca.creator_size}},
                        "sources": [
                            {
                                "name": {
                                    "terms": {
                                        "field": "sp.name"
                                    }
                                }
                            },
                            {
                                "uri": {
                                    "terms": {
                                        "field": "sp.uri"
                                    }
                                }
                            }
                        ]
                    },
                    "aggs": {
                        "ca_reverse": {
                            "reverse_nested": {},
                            "aggs": {
                                "ca_count": {
                                    "cardinality": {
                                        "field": "root_uri"
                                    }
                                }
                            }
                        }
                    }
                }
            }
        },
        "sc_filter": {
            "nested": {
                "path": "sc"
            },
            "aggs": {
                "sc_count": {
                    "cardinality": {
                        "field": "sc.uri"
                    }
                },
                "sc_buckets": {
                    "composite": {
                        "size": {{ca.holder_size}}{{^ca.holder_size}}5{{/ca.holder_size}},
                        "sources": [
                            {
                                "name": {
                                    "terms": {
                                        "field": "sc.name"
                                    }
                                }
                            },
                            {
                                "uri": {
                                    "terms": {
                                        "field": "sc.uri"
                                    }
                                }
                            }
                        ]
                    },
                    "aggs": {
                        "ca_reverse": {
                            "reverse_nested": {},
                            "aggs": {
                                "ca_count": {
                                    "cardinality": {
                                        "field": "root_uri"
                                    }
                                }
                            }
                        }
                    }
                }
            }
        },
        "province_filter": {
            "nested": {
                "path": "sc"
            },
            "aggs": {
                "province_count": {
                    "cardinality": {
                        "field": "sc.province"
                    }
                },
                "province_buckets": {
                    "terms": {
                        "field": "sc.province",
                        "order": {
                            "_key": "asc"
                        },
                        "size": {{ca.province_size}}{{^ca.province_size}}5{{/ca.province_size}}
                    },
                    "aggs": {
                        "ca_reverse": {
                            "reverse_nested": {},
                            "aggs": {
                                "ca_count": {
                                    "cardinality": {
                                        "field": "root_uri"
                                    }
                                }
                            }
                        }
                    }
                }
            }
        },
        "datefrom_filter": {
            "filter": {
                "exists": {
                    "field": "century_from"
                }
            },
            "aggs": {
                "century_count": {
                    "cardinality": {
                        "field": "century_from"
                    }
                },
                "century_buckets": {
                    "terms": {
                        "field": "century_from",
                        "size": {{ca.century_from_size}}{{^ca.century_from_size}}5{{/ca.century_from_size}},
                        "order": {
                            "_key": "asc"
                        }
                    },
                    "aggs": {
                        "ca_count": {
                            "cardinality": {
                                "field": "root_uri"
                            }
                        },
                        "quarter_buckets": {
                            "terms": {
                                "field": "century_quarter_from",
                                "order": {
                                    "_key": "asc"
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
                    }
                }
            }
        },
        "dateto_filter": {
            "filter": {
                "exists": {
                    "field": "century_to"
                }
            },
            "aggs": {
                "century_count": {
                    "cardinality": {
                        "field": "century_to"
                    }
                },
                "century_buckets": {
                    "terms": {
                        "field": "century_to",
                        "size": {{ca.century_to_size}}{{^ca.century_to_size}}5{{/ca.century_to_size}},
                        "order": {
                            "_key": "asc"
                        }
                    },
                    "aggs": {
                        "ca_count": {
                            "cardinality": {
                                "field": "root_uri"
                            }
                        },
                        "quarter_buckets": {
                            "terms": {
                                "field": "century_quarter_to",
                                "order": {
                                    "_key": "asc"
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
                    }
                }
            }
        },
        "ca_buckets": {
            "composite": {
                "size": {{ca.size}}{{^ca.size}}5{{/ca.size}},
                {{#ca.after}}
                "after": {
                    "name": "{{ca.after.name}}",
                    "uri": "{{ca.after.uri}}"
                },
                {{/ca.after}}
                "sources": [
                    {
                        "name": {
                            "terms": {
                                "field": "root_name"
                            }
                        }
                    },
                    {
                        "uri": {
                            "terms": {
                                "field": "root_uri"
                            }
                        }
                    }
                ]
            },
            "aggs": {
                "ca_filter": {
                    "filter": {
                        "bool": {
                            "filter": [
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
                                }
                                {{/ca.query}}
                            ]
                        }
                    },
                    "aggs": {
                        "ca_type": {
                            "terms": {
                                "field": "type"
                            },
                            "aggs": {
                                "ca_type_count": {
                                    "cardinality": {
                                        "field": "uri"
                                    }
                                }
                            }
                        }
                    }
                },
                "uad_nested": {
                    "nested": {
                        "path": "uad"
                    },
                    "aggs": {
                        "uad_filter": {
                            "filter": {
                                "bool": {
                                    "filter": [
                                        {{#ca.query}}
                                        {
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
                                        {{/ca.query}}
                                    ]
                                }
                            },
                            "aggs": {
                                "uad_count": {
                                    "cardinality": {
                                        "field": "uad.uri"
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
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
| $.id | Mandatorio | Stringa | Identificativo del template di ricerca | Costante pari a "arc_G1100" |
| $.params | Mandatorio | Oggetto | Contenitore dei parametri | |
| $.params.ca | Mandatorio | Oggetto | Contenitore dei parametri di ricerca per le entità  di tipo "Complesso archivistico". | |
| $.params.ca.size | Facoltativo | Intero | Numero di documenti restituiti per pagina. | |
| $.params.ca.century_from_size | Facoltativo | Intero | Numero di elementi mostrati nella faccetta "Periodo Da" | |
| $.params.ca.century_to_size | Facoltativo | Intero | Numero di elementi mostrati nella faccetta "Periodo A" | |
| $.params.ca.province_size | Facoltativo | Intero | Numero di elementi mostrati nella faccetta "Provincia" | |
| $.params.ca.creator_size | Facoltativo | Intero | Numero di elementi mostrati nella faccetta "Soggetto Produttore" | |
| $.params.ca.holder.size | Facoltativo | Intero | Numero di elementi mostrati nella faccetta "Soggetto Conservatore" | |
| $.params.ca.after | Facoltativo | Oggetto | Contenitore dei parametri di identificazione dell'ultimo documento letto per la paginazione. | Da inserire al fine di scorrere le pagine dei risultati |
| $.params.ca.after.name | Facoltativo | Stringa | Denominazione dell'ultimo complesso archivistico radice dell'ultima pagina restituita. | Valore desumibile dall'ultima pagina di documenti letti |
| $.params.ca.after.uri | Facoltativo | Stringa | Identificativo dell'ultimo complesso archivistico radice dell'ultima pagina restituita. | Valore desumibile dall'ultima pagina di documenti letti |
| $.params.ca.query | Facoltativo | Stringa | Stringa di ricerca. | Da inserire solo se valorizzato il filtro "Cerca". |
| $.params.ca.province | Facoltativo | Oggetto | Contenitore dei parametri che identificano le province di interesse. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Provincia". |
| $.params.ca.province.provinces | Facoltativo | Vettore di stringhe | Vettore costituito dalle province selezionate | Da inserire solo se risulta selezionato almeno un valore del filtro "Provincia". Utilizzare le chiavi associate ai valori selezionati. |
| $.params.ca.century_from | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo Da". |
| $.params.ca.century_from.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo da". |
| $.params.ca.century_quarter_from | Facoltativo | Oggetto | Contenitore dei parametri che identificano il quarto di secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Venticinquennio Da". |
| $.params.ca.century_quarter_from.quarters | Facoltativo | Vettore di stringhe | Quarto di secolo dell'estremo anteriore del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Venticinquennio da". |
| $.params.ca.century_to | Facoltativo | Oggetto | Contenitore dei parametri che identificano il secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Periodo a". |
| $.params.ca.century_to.centuries | Facoltativo | Vettore di stringhe | Secolo dell'estremo recente del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Periodo a". |
| $.params.ca.century_quarter_to | Facoltativo | Oggetto | Contenitore dei parametri che identificano il quarto di secolo dell'estremo remoto del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Venticinquennio A". |
| $.params.ca.century_quarter_to.quarters | Facoltativo | Vettore di stringhe | Quarto di secolo dell'estremo remoto del periodo di esistenza dell'entità di riferimento. | Da inserire solo se risulta selezionato almeno un valore del filtro "Venticinquennio A". |
| $.params.ca.creator | Facoltativo | Oggetto | Contenitore dei parametri che identificano il soggetto produttore del complesso archivistico. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Soggetto produttore". |
| $.params.ca.creator.creators | Facoltativo | Vettore di stringhe | Vettore costituito dagli identificativi dei Soggetti produttori selezionati. | Da inserire solo se risulta selezionato almeno un valore del filtro "Soggetto produttore". |
| $.params.ca.holder | Facoltativo | Oggetto | Contenitore dei parametri che identificano il soggetto conservatore del complesso archivistico. | Da inserire solo se risulta selezionato almeno un valore per il filtro "Soggetto conservatore". |
| $.params.ca.holder.holders | Facoltativo | Vettore di stringhe | Vettore costituito dagli identificativi dei Soggetti conservatori selezionati. | Da inserire solo se risulta selezionato almeno un valore del filtro "Soggetto produttore". |

Di seguito un body di esempio.

<details>
<summary>Espandi</summary>
<p>

```JSON
{
    "id": "arc_G1100",
    "params": {
        "ca": {
            "size": 5,
            "century_from_size": 5,
            "century_to_size": 5,
            "province_size": 5,
            "creator_size": 5,
            "holder_size": 5,
            "after": {
                "name":"Centro studi Gerardo Dottori",
                "uri":"FN3"
            },
            "query": "cartolina",
            "century_from": {
                "centuries": [
                    "1901-2000"
                ]
            },
            "century_quarter_from": {
                "quarters": [
                    "1901-1925"
                ]
            },
            "century_to": {
                "centuries": [
                    "1901-2000"
                ]
            },
            "century_quarter_to": {
                "quarters": [
                    "1976-2000"
                ]
            },
            "province": {
                "provinces": [
                    "NA",
                    "SA"
                ]
            },
            "creator": {
                "creators": [
                    "SP1",
                    "SP2",
                    "SP3",
                    "SP4"
                ]
            },
            "holder": {
                "holders": [
                    "SC1",
                    "SC2"
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
| Json Path | Tipo | Descrizione | Faccetta |
|-|-|-|-|
| $.aggregations.ca_count.value | Intero | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati. | |
| $.aggregations.ca_buckets.after_key | Oggetto | Contenitore dei parametri che identificano l'ultimo complesso archivistico radice resituito nella pagina corrente (necessario per una corretta paginazione) | |
| $.aggregations.ca_buckets.after_key.name | Stringa | Denominazione dell'ultimo complesso archivistico radice della pagina. | |
| $.aggregations.ca_buckets.after_key.uri | Stringa | Identificativo dell'ultimo complesso archivistico radice della pagina. | |
| $.aggregations.ca_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze dei complessi archivistici radice restituiti, corredati dai relativi conteggi. | |
| $.aggregations.ca_buckets.buckets[i].key | Oggetto | Contenitore dei parametri che identificano l'i-esimo complesso archivistico radice. | |
| $.aggregations.ca_buckets.buckets[i].key.name | Stringa | Denominazione dell'i-esimo complesso archivistico radice. | |
| $.aggregations.ca_buckets.buckets[i].key.uri | Stringa | Identificativo dell'i-esimo complesso archivistico radice. | |
| $.aggregations.ca_buckets.buckets[i].ca_filter.ca_type.buckets | Vettore di oggetti | Vettore contenente i diversi tipi di complessi archivistici contenuti nell'i-esimo complesso archivistico radice e soddisfacenti i criteri di ricerca impostati, corredati dai relativi conteggi| |
| $.aggregations.ca_buckets.buckets[i].ca_filter.ca_type.buckets[j].key | Stringa | J-esimo tipo di complesso archivistico contenuto nell'i-esimo complesso archivistico radice e soddisfacente i criteri di ricerca impostati. | |
| $.aggregations.ca_buckets.buckets[i].ca_filter.ca_type.buckets[j].ca_type_count.value | Intero | Conteggio distinto dei complessi archivistici di j-esimo tipo contenuti nell'i-esimo complesso archivistico radice e soddisfacenti i criteri di ricerca impostati. | |
| $.aggregations.ca_buckets.buckets[i].uad_nested.uad_filter.uad_count.value | Intero | Conteggio distinto delle unità archivistiche / documentarie contenute nell'i-esimo complesso archivistico radice e soddisfacenti i criteri di ricerca impostati.| |
| $.aggregations.sc_filter.sc_count.value | Intero | Conteggio distinto dei soggetti conservatori associati ai complessi archivistici restituiti. | Soggetti Conservatori |
| $.aggregations.sc_filter.sc_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze dei soggetti conservatori associati ai complessi archivistici restituiti, corredate dai relativi conteggi. | Soggetti Conservatori |
| $.aggregations.sc_filter.sc_buckets.buckets[i].key | Oggetto | Contenitore dei parametri che identificano l'i-esimo soggetto conservatore. | Soggetti Conservatori |
| $.aggregations.sc_filter.sc_buckets.buckets[i].key.name | Stringa | Denominazione dell'i-esimo soggetto conservatore. | Soggetti Conservatori |
| $.aggregations.sc_filter.sc_buckets.buckets[i].key.uri | Stringa | Identificativo dell'i-esimo soggetto conservatore. | Soggetti Conservatori |
| $.aggregations.sc_filter.sc_buckets.buckets[i].ca_reverse.ca_count.value | Intero | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati e associati all'i-esimo soggetto conservatore. | Soggetti Conservatori |
| $.aggregations.sp_filter.sp_count.value | Intero | Conteggio distinto dei soggetti produttori associati ai complessi archivistici restituiti. | Soggetti Produttori |
| $.aggregations.sp_filter.sp_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze dei soggetti produttori associati ai complessi archivistici restituiti, corredate dai relativi conteggi. | Soggetti Produttori |
| $.aggregations.sp_filter.sp_buckets.buckets[i].key | Oggetto | Contenitore dei parametri che identificano l'i-esimo soggetto produttore. | Soggetti Produttori |
| $.aggregations.sp_filter.sp_buckets.buckets[i].key.name | Stringa | Denominazione dell'i-esimo soggetto produttore. | Soggetti Produttori |
| $.aggregations.sp_filter.sp_buckets.buckets[i].key.uri | Stringa | Identificativo dell'i-esimo soggetto produttore. | Soggetti Produttori |
| $.aggregations.sp_filter.sp_buckets.buckets[i].ca_reverse.ca_count.value | Intero | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati e associati all'i-esimo soggetto produttore. | Soggetti Produttori |
| $.aggregations.province_filter.province_count.value | Intero | Conteggio distinto dele province associate ai complessi archivistici restituiti. | Provincia |
| $.aggregations.province_filter.province_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze delle province associate ai complessi archivistici restituiti, corredate dai relativi conteggi. | Provincia |
| $.aggregations.province_filter.province_buckets.buckets[i].key | Stringa | Identificativo dell'i-esima provincia. | Provincia |
| $.aggregations.province_filter.province_buckets.buckets[i].ca_reverse.ca_count.value | Intero | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati e associati all'i-esima provincia. | Provincia |
| $.aggregations.datefrom_filter.century_count.value | Intero | Conteggio distinto dei secoli degli estremi di esistenza remoti dei complessi archivistici restituiti. | Periodo Da |
| $.aggregations.datefrom_filter.century_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze dei secoli degli estremi di esistenza remoti dei complessi archivistici restituiti, corredati dai relativi conteggi. | Periodo Da |
| $.aggregations.datefrom_filter.century_buckets.buckets[i].key | Stringa | Identificativo dell'i-esimo secolo. | Periodo Da |
| $.aggregations.datefrom_filter.century_buckets.buckets[i].ca_count.value | Stringa | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati e con estremo di esistenza remoto ricadente nell'i-esimo secolo. | Periodo Da |
| $.aggregations.datefrom_filter.century_buckets.buckets[i].quarter_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze dei quarti dell'i-esimo secolo degli estremi di esistenza remoti dei complessi archivistici restituiti, corredati dai relativi conteggi. | Periodo Da |
| $.aggregations.datefrom_filter.century_buckets.buckets[i].quarter_buckets.buckets[j].key | Stringa | Identificativo del j-esimo quarto dell'i-esimo secolo. | Periodo Da |
| $.aggregations.datefrom_filter.century_buckets.buckets[i].quarter_buckets.buckets[j].ca_count.value | Stringa | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati e con estremo di esistenza remoto ricadente nel j-esimo quarto dell'i-esimo secolo. | Periodo Da |
| $.aggregations.dateto_filter.century_count.value | Intero | Conteggio distinto dei secoli degli estremi di esistenza recenti dei complessi archivistici restituiti. | Periodo A |
| $.aggregations.dateto_filter.century_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze dei secoli degli estremi di esistenza recenti dei complessi archivistici restituiti, corredati dai relativi conteggi. | Periodo A |
| $.aggregations.dateto_filter.century_buckets.buckets[i].key | Stringa | Identificativo dell'i-esimo secolo. | Periodo A |
| $.aggregations.dateto_filter.century_buckets.buckets[i].ca_count.value | Stringa | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati e con estremo di esistenza recente ricadente nell'i-esimo secolo. | Periodo A |
| $.aggregations.dateto_filter.century_buckets.buckets[i].quarter_buckets.buckets | Vettore di oggetti | Vettore contenente le occorrenze dei quarti dell'i-esimo secolo degli estremi di esistenza recenti dei complessi archivistici restituiti, corredati dai relativi conteggi. | Periodo A |
| $.aggregations.dateto_filter.century_buckets.buckets[i].quarter_buckets.buckets[j].key | Stringa | Identificativo del j-esimo quarto dell'i-esimo secolo. | Periodo A |
| $.aggregations.dateto_filter.century_buckets.buckets[i].quarter_buckets.buckets[j].ca_count.value | Stringa | Conteggio distinto dei complessi archivistici radice che contengono complessi archivistici o unità archivistiche / documentarie soddisfacenti i criteri di ricerca impostati e con estremo di esistenza recente ricadente nel j-esimo quarto dell'i-esimo secolo. | Periodo A |




Di seguito una risposta di esempio.

<details>
<summary>Espandi</summary>
<p>

```JSON
{
    "took": 23,
    "timed_out": false,
    "_shards": {
        "total": 4,
        "successful": 4,
        "skipped": 0,
        "failed": 0
    },
    "hits": {
        "total": {
            "value": 2,
            "relation": "eq"
        },
        "max_score": null,
        "hits": []
    },
    "aggregations": {
        "sp_filter": {
            "doc_count": 2,
            "sp_count": {
                "value": 1
            },
            "sp_buckets": {
                "after_key": {
                    "name": "Dottori Gerardo",
                    "uri": "SP4"
                },
                "buckets": [
                    {
                        "key": {
                            "name": "Dottori Gerardo",
                            "uri": "SP4"
                        },
                        "doc_count": 2,
                        "ca_reverse": {
                            "doc_count": 2,
                            "ca_count": {
                                "value": 1
                            }
                        }
                    }
                ]
            }
        },
        "province_filter": {
            "doc_count": 2,
            "province_buckets": {
                "doc_count_error_upper_bound": 0,
                "sum_other_doc_count": 0,
                "buckets": [
                    {
                        "key": "SA",
                        "doc_count": 2,
                        "ca_reverse": {
                            "doc_count": 2,
                            "ca_count": {
                                "value": 1
                            }
                        }
                    }
                ]
            },
            "province_count": {
                "value": 1
            }
        },
        "datefrom_filter": {
            "doc_count": 2,
            "century_count": {
                "value": 1
            },
            "century_buckets": {
                "doc_count_error_upper_bound": 0,
                "sum_other_doc_count": 0,
                "buckets": [
                    {
                        "key": "1901-2000",
                        "doc_count": 2,
                        "ca_count": {
                            "value": 1
                        },
                        "quarter_buckets": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": [
                                {
                                    "key": "1901-1925",
                                    "doc_count": 2,
                                    "ca_count": {
                                        "value": 1
                                    }
                                }
                            ]
                        }
                    }
                ]
            }
        },
        "dateto_filter": {
            "doc_count": 2,
            "century_count": {
                "value": 1
            },
            "century_buckets": {
                "doc_count_error_upper_bound": 0,
                "sum_other_doc_count": 0,
                "buckets": [
                    {
                        "key": "1901-2000",
                        "doc_count": 2,
                        "ca_count": {
                            "value": 1
                        },
                        "quarter_buckets": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": [
                                {
                                    "key": "1976-2000",
                                    "doc_count": 2,
                                    "ca_count": {
                                        "value": 1
                                    }
                                }
                            ]
                        }
                    }
                ]
            }
        },
        "ca_count": {
            "value": 1
        },
        "ca_buckets": {
            "after_key": {
                "name": "Centro studi Gerardo Dottori",
                "uri": "FN3"
            },
            "buckets": [
                {
                    "key": {
                        "name": "Centro studi Gerardo Dottori",
                        "uri": "FN3"
                    },
                    "doc_count": 2,
                    "uad_nested": {
                        "doc_count": 8,
                        "uad_filter": {
                            "doc_count": 6,
                            "uad_count": {
                                "value": 3
                            }
                        }
                    },
                    "ca_filter": {
                        "doc_count": 2,
                        "ca_type": {
                            "doc_count_error_upper_bound": 0,
                            "sum_other_doc_count": 0,
                            "buckets": [
                                {
                                    "key": "fondo",
                                    "doc_count": 1,
                                    "ca_type_count": {
                                        "value": 1
                                    }
                                },
                                {
                                    "key": "serie",
                                    "doc_count": 1,
                                    "ca_type_count": {
                                        "value": 1
                                    }
                                }
                            ]
                        }
                    }
                }
            ]
        },
        "sc_filter": {
            "doc_count": 2,
            "sc_count": {
                "value": 1
            },
            "sc_buckets": {
                "after_key": {
                    "name": "privato",
                    "uri": "SC2"
                },
                "buckets": [
                    {
                        "key": {
                            "name": "privato",
                            "uri": "SC2"
                        },
                        "doc_count": 2,
                        "ca_reverse": {
                            "doc_count": 2,
                            "ca_count": {
                                "value": 1
                            }
                        }
                    }
                ]
            }
        }
    }
}
```

</p>
</details>
