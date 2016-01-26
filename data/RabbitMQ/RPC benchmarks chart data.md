## ONE-WAY RPC BENCHMARKS CHART DATA ##

**One Publisher, One Consumer**  
**Non-Persistent Messaging** *  
**Message Size:** 2048 bytes (roughly) each way  
**Messages Per Thread**: 5000  
**Serialization Format**: JSON  
**Publisher Confirms:** Off *  
**Consumer No-Ack:** False *  
**Consumer Prefetch:** 50   
**Client logging:** Off



| *                                        | AVERAGE TIME PER THREAD |           |           |           |   | THROUGHPUT (Messages Per Second) |         |         |         |   | THROUGHPUT (KB Per Second) |          |          |          |
|------------------------------------------|-------------------------|-----------|-----------|-----------|---|----------------------------------|---------|---------|---------|---|----------------------------|----------|----------|----------|
|                                          |                         |           |           |           |   |                                  |         |         |         |   |                            |          |          |          |
|                                          | 10                      | 20        | 40        | 80        |   | 10                               | 20      | 40      | 80      |   | 10                         | 20       | 40       | 80       |
| RestBus (Web API)                        | 8.26645                 | 12.2151   | 23.08605  | 49.60125  |   | 6048.55                          | 8186.59 | 8663.24 | 8064.31 |   | 12097.09                   | 16373.18 | 17326.48 | 16128.63 |
| RestBus (ASP.NET 5)                      | 8.3271                  | 11.4928   | 23.32335  | 49.51375  |   | 6004.49                          | 8701.1  | 8575.1  | 8078.56 |   | 12008.98                   | 17402.2  | 17150.19 | 16157.13 |
| RestBus (ASP.NET 5 -- Bare to the metal) | 7.59385                 | 11.3704   | 23.00495  | 49.1578   |   | 6584.28                          | 8794.77 | 8693.78 | 8137.06 |   | 13168.55                   | 17589.53 | 17387.56 | 16274.12 |
| EasyNetQ                                 | 8.7731                  | 13.0456   | 23.8614   | 51.8716   |   | 5699.24                          | 7665.42 | 8381.74 | 7711.35 |   | 11398.48                   | 15330.84 | 16763.48 | 15422.7  |
| MassTransit                              | 28.12595                | 35.35455  | 51.30155  | 87.26165  |   | 1777.72                          | 2828.49 | 3898.52 | 4583.92 |   | 3555.44                    | 5656.98  | 7797.04  | 9167.83  |
| NServiceBus                              | 85.9955                 | 171.72645 | 341.91375 | 697.73085 |   | 581.43                           | 582.32  | 584.94  | 573.29  |   | 1162.85                    | 1164.64  | 1169.89  | 1146.57  |