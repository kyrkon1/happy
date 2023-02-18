---
title: "2021 Analysis"
author: "Harika Kovvuri"
date: "2023-02-18"
output: 
  html_document: 
    keep_md: yes
---



#Load Programs

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.1 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(naniar)
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
library(here)
```

```
## here() starts at /Users/harikakovvuri/Desktop/happy-main
```

#Load Data

```r
happy <-read.csv("/Users/harikakovvuri/Desktop/2021.csv")
happy
```

```
##                  Country.name                 Regional.indicator Ladder.score
## 1                     Finland                     Western Europe        7.842
## 2                     Denmark                     Western Europe        7.620
## 3                 Switzerland                     Western Europe        7.571
## 4                     Iceland                     Western Europe        7.554
## 5                 Netherlands                     Western Europe        7.464
## 6                      Norway                     Western Europe        7.392
## 7                      Sweden                     Western Europe        7.363
## 8                  Luxembourg                     Western Europe        7.324
## 9                 New Zealand              North America and ANZ        7.277
## 10                    Austria                     Western Europe        7.268
## 11                  Australia              North America and ANZ        7.183
## 12                     Israel       Middle East and North Africa        7.157
## 13                    Germany                     Western Europe        7.155
## 14                     Canada              North America and ANZ        7.103
## 15                    Ireland                     Western Europe        7.085
## 16                 Costa Rica        Latin America and Caribbean        7.069
## 17             United Kingdom                     Western Europe        7.064
## 18             Czech Republic         Central and Eastern Europe        6.965
## 19              United States              North America and ANZ        6.951
## 20                    Belgium                     Western Europe        6.834
## 21                     France                     Western Europe        6.690
## 22                    Bahrain       Middle East and North Africa        6.647
## 23                      Malta                     Western Europe        6.602
## 24   Taiwan Province of China                          East Asia        6.584
## 25       United Arab Emirates       Middle East and North Africa        6.561
## 26               Saudi Arabia       Middle East and North Africa        6.494
## 27                      Spain                     Western Europe        6.491
## 28                      Italy                     Western Europe        6.483
## 29                   Slovenia         Central and Eastern Europe        6.461
## 30                  Guatemala        Latin America and Caribbean        6.435
## 31                    Uruguay        Latin America and Caribbean        6.431
## 32                  Singapore                     Southeast Asia        6.377
## 33                     Kosovo         Central and Eastern Europe        6.372
## 34                   Slovakia         Central and Eastern Europe        6.331
## 35                     Brazil        Latin America and Caribbean        6.330
## 36                     Mexico        Latin America and Caribbean        6.317
## 37                    Jamaica        Latin America and Caribbean        6.309
## 38                  Lithuania         Central and Eastern Europe        6.255
## 39                     Cyprus                     Western Europe        6.223
## 40                    Estonia         Central and Eastern Europe        6.189
## 41                     Panama        Latin America and Caribbean        6.180
## 42                 Uzbekistan Commonwealth of Independent States        6.179
## 43                      Chile        Latin America and Caribbean        6.172
## 44                     Poland         Central and Eastern Europe        6.166
## 45                 Kazakhstan Commonwealth of Independent States        6.152
## 46                    Romania         Central and Eastern Europe        6.140
## 47                     Kuwait       Middle East and North Africa        6.106
## 48                     Serbia         Central and Eastern Europe        6.078
## 49                El Salvador        Latin America and Caribbean        6.061
## 50                  Mauritius                 Sub-Saharan Africa        6.049
## 51                     Latvia         Central and Eastern Europe        6.032
## 52                   Colombia        Latin America and Caribbean        6.012
## 53                    Hungary         Central and Eastern Europe        5.992
## 54                   Thailand                     Southeast Asia        5.985
## 55                  Nicaragua        Latin America and Caribbean        5.972
## 56                      Japan                          East Asia        5.940
## 57                  Argentina        Latin America and Caribbean        5.929
## 58                   Portugal                     Western Europe        5.929
## 59                   Honduras        Latin America and Caribbean        5.919
## 60                    Croatia         Central and Eastern Europe        5.882
## 61                Philippines                     Southeast Asia        5.880
## 62                South Korea                          East Asia        5.845
## 63                       Peru        Latin America and Caribbean        5.840
## 64     Bosnia and Herzegovina         Central and Eastern Europe        5.813
## 65                    Moldova Commonwealth of Independent States        5.766
## 66                    Ecuador        Latin America and Caribbean        5.764
## 67                 Kyrgyzstan Commonwealth of Independent States        5.744
## 68                     Greece                     Western Europe        5.723
## 69                    Bolivia        Latin America and Caribbean        5.716
## 70                   Mongolia                          East Asia        5.677
## 71                   Paraguay        Latin America and Caribbean        5.653
## 72                 Montenegro         Central and Eastern Europe        5.581
## 73         Dominican Republic        Latin America and Caribbean        5.545
## 74               North Cyprus                     Western Europe        5.536
## 75                    Belarus Commonwealth of Independent States        5.534
## 76                     Russia Commonwealth of Independent States        5.477
## 77  Hong Kong S.A.R. of China                          East Asia        5.477
## 78                 Tajikistan Commonwealth of Independent States        5.466
## 79                    Vietnam                     Southeast Asia        5.411
## 80                      Libya       Middle East and North Africa        5.410
## 81                   Malaysia                     Southeast Asia        5.384
## 82                  Indonesia                     Southeast Asia        5.345
## 83        Congo (Brazzaville)                 Sub-Saharan Africa        5.342
## 84                      China                          East Asia        5.339
## 85                Ivory Coast                 Sub-Saharan Africa        5.306
## 86                    Armenia Commonwealth of Independent States        5.283
## 87                      Nepal                         South Asia        5.269
## 88                   Bulgaria         Central and Eastern Europe        5.266
## 89                   Maldives                         South Asia        5.198
## 90                 Azerbaijan Commonwealth of Independent States        5.171
## 91                   Cameroon                 Sub-Saharan Africa        5.142
## 92                    Senegal                 Sub-Saharan Africa        5.132
## 93                    Albania         Central and Eastern Europe        5.117
## 94            North Macedonia         Central and Eastern Europe        5.101
## 95                      Ghana                 Sub-Saharan Africa        5.088
## 96                      Niger                 Sub-Saharan Africa        5.074
## 97               Turkmenistan Commonwealth of Independent States        5.066
## 98                     Gambia                 Sub-Saharan Africa        5.051
## 99                      Benin                 Sub-Saharan Africa        5.045
## 100                      Laos                     Southeast Asia        5.030
## 101                Bangladesh                         South Asia        5.025
## 102                    Guinea                 Sub-Saharan Africa        4.984
## 103              South Africa                 Sub-Saharan Africa        4.956
## 104                    Turkey       Middle East and North Africa        4.948
## 105                  Pakistan                         South Asia        4.934
## 106                   Morocco       Middle East and North Africa        4.918
## 107                 Venezuela        Latin America and Caribbean        4.892
## 108                   Georgia Commonwealth of Independent States        4.891
## 109                   Algeria       Middle East and North Africa        4.887
## 110                   Ukraine Commonwealth of Independent States        4.875
## 111                      Iraq       Middle East and North Africa        4.854
## 112                     Gabon                 Sub-Saharan Africa        4.852
## 113              Burkina Faso                 Sub-Saharan Africa        4.834
## 114                  Cambodia                     Southeast Asia        4.830
## 115                Mozambique                 Sub-Saharan Africa        4.794
## 116                   Nigeria                 Sub-Saharan Africa        4.759
## 117                      Mali                 Sub-Saharan Africa        4.723
## 118                      Iran       Middle East and North Africa        4.721
## 119                    Uganda                 Sub-Saharan Africa        4.636
## 120                   Liberia                 Sub-Saharan Africa        4.625
## 121                     Kenya                 Sub-Saharan Africa        4.607
## 122                   Tunisia       Middle East and North Africa        4.596
## 123                   Lebanon       Middle East and North Africa        4.584
## 124                   Namibia                 Sub-Saharan Africa        4.574
## 125   Palestinian Territories       Middle East and North Africa        4.517
## 126                   Myanmar                     Southeast Asia        4.426
## 127                    Jordan       Middle East and North Africa        4.395
## 128                      Chad                 Sub-Saharan Africa        4.355
## 129                 Sri Lanka                         South Asia        4.325
## 130                 Swaziland                 Sub-Saharan Africa        4.308
## 131                   Comoros                 Sub-Saharan Africa        4.289
## 132                     Egypt       Middle East and North Africa        4.283
## 133                  Ethiopia                 Sub-Saharan Africa        4.275
## 134                Mauritania                 Sub-Saharan Africa        4.227
## 135                Madagascar                 Sub-Saharan Africa        4.208
## 136                      Togo                 Sub-Saharan Africa        4.107
## 137                    Zambia                 Sub-Saharan Africa        4.073
## 138              Sierra Leone                 Sub-Saharan Africa        3.849
## 139                     India                         South Asia        3.819
## 140                   Burundi                 Sub-Saharan Africa        3.775
## 141                     Yemen       Middle East and North Africa        3.658
## 142                  Tanzania                 Sub-Saharan Africa        3.623
## 143                     Haiti        Latin America and Caribbean        3.615
## 144                    Malawi                 Sub-Saharan Africa        3.600
## 145                   Lesotho                 Sub-Saharan Africa        3.512
## 146                  Botswana                 Sub-Saharan Africa        3.467
## 147                    Rwanda                 Sub-Saharan Africa        3.415
## 148                  Zimbabwe                 Sub-Saharan Africa        3.145
## 149               Afghanistan                         South Asia        2.523
##     Standard.error.of.ladder.score upperwhisker lowerwhisker
## 1                            0.032        7.904        7.780
## 2                            0.035        7.687        7.552
## 3                            0.036        7.643        7.500
## 4                            0.059        7.670        7.438
## 5                            0.027        7.518        7.410
## 6                            0.035        7.462        7.323
## 7                            0.036        7.433        7.293
## 8                            0.037        7.396        7.252
## 9                            0.040        7.355        7.198
## 10                           0.036        7.337        7.198
## 11                           0.041        7.265        7.102
## 12                           0.034        7.224        7.090
## 13                           0.040        7.232        7.077
## 14                           0.042        7.185        7.021
## 15                           0.040        7.164        7.006
## 16                           0.056        7.179        6.960
## 17                           0.038        7.138        6.990
## 18                           0.049        7.062        6.868
## 19                           0.049        7.047        6.856
## 20                           0.034        6.901        6.767
## 21                           0.037        6.762        6.618
## 22                           0.068        6.779        6.514
## 23                           0.044        6.688        6.516
## 24                           0.038        6.659        6.510
## 25                           0.039        6.637        6.484
## 26                           0.056        6.604        6.384
## 27                           0.042        6.574        6.408
## 28                           0.045        6.572        6.395
## 29                           0.043        6.546        6.376
## 30                           0.073        6.577        6.292
## 31                           0.046        6.521        6.341
## 32                           0.043        6.460        6.293
## 33                           0.059        6.487        6.257
## 34                           0.041        6.411        6.251
## 35                           0.043        6.415        6.245
## 36                           0.053        6.420        6.213
## 37                           0.156        6.615        6.004
## 38                           0.045        6.344        6.167
## 39                           0.049        6.319        6.128
## 40                           0.038        6.263        6.115
## 41                           0.073        6.323        6.036
## 42                           0.068        6.312        6.045
## 43                           0.046        6.262        6.081
## 44                           0.040        6.245        6.087
## 45                           0.047        6.243        6.060
## 46                           0.057        6.253        6.027
## 47                           0.066        6.235        5.977
## 48                           0.053        6.181        5.974
## 49                           0.065        6.188        5.933
## 50                           0.059        6.165        5.933
## 51                           0.036        6.103        5.961
## 52                           0.061        6.132        5.892
## 53                           0.047        6.085        5.899
## 54                           0.047        6.077        5.893
## 55                           0.083        6.134        5.810
## 56                           0.040        6.020        5.861
## 57                           0.056        6.040        5.819
## 58                           0.055        6.037        5.821
## 59                           0.082        6.081        5.758
## 60                           0.048        5.975        5.788
## 61                           0.052        5.982        5.778
## 62                           0.042        5.928        5.763
## 63                           0.075        5.988        5.692
## 64                           0.050        5.911        5.715
## 65                           0.046        5.856        5.677
## 66                           0.057        5.875        5.653
## 67                           0.046        5.834        5.653
## 68                           0.046        5.813        5.632
## 69                           0.053        5.819        5.613
## 70                           0.042        5.760        5.595
## 71                           0.092        5.832        5.473
## 72                           0.054        5.686        5.475
## 73                           0.071        5.685        5.405
## 74                           0.051        5.636        5.435
## 75                           0.047        5.625        5.442
## 76                           0.033        5.541        5.413
## 77                           0.049        5.573        5.380
## 78                           0.034        5.532        5.400
## 79                           0.039        5.488        5.334
## 80                           0.076        5.558        5.262
## 81                           0.049        5.480        5.289
## 82                           0.056        5.454        5.235
## 83                           0.097        5.533        5.151
## 84                           0.029        5.397        5.281
## 85                           0.078        5.460        5.152
## 86                           0.058        5.397        5.168
## 87                           0.070        5.406        5.132
## 88                           0.054        5.371        5.160
## 89                           0.072        5.339        5.057
## 90                           0.040        5.250        5.091
## 91                           0.074        5.288        4.996
## 92                           0.068        5.266        4.998
## 93                           0.059        5.234        5.001
## 94                           0.051        5.202        5.001
## 95                           0.067        5.219        4.958
## 96                           0.102        5.273        4.875
## 97                           0.036        5.136        4.996
## 98                           0.089        5.225        4.877
## 99                           0.073        5.189        4.901
## 100                          0.045        5.119        4.941
## 101                          0.046        5.115        4.934
## 102                          0.090        5.160        4.808
## 103                          0.060        5.074        4.839
## 104                          0.046        5.038        4.857
## 105                          0.068        5.066        4.802
## 106                          0.060        5.036        4.800
## 107                          0.064        5.017        4.767
## 108                          0.054        4.998        4.785
## 109                          0.053        4.991        4.783
## 110                          0.052        4.977        4.773
## 111                          0.059        4.970        4.738
## 112                          0.075        4.998        4.706
## 113                          0.081        4.993        4.675
## 114                          0.067        4.963        4.698
## 115                          0.103        4.997        4.592
## 116                          0.052        4.861        4.658
## 117                          0.082        4.884        4.563
## 118                          0.055        4.828        4.614
## 119                          0.073        4.780        4.493
## 120                          0.106        4.833        4.417
## 121                          0.072        4.747        4.466
## 122                          0.058        4.709        4.484
## 123                          0.055        4.691        4.477
## 124                          0.064        4.700        4.448
## 125                          0.067        4.649        4.384
## 126                          0.052        4.527        4.324
## 127                          0.062        4.516        4.273
## 128                          0.094        4.540        4.171
## 129                          0.066        4.454        4.196
## 130                          0.071        4.448        4.168
## 131                          0.084        4.454        4.123
## 132                          0.045        4.371        4.195
## 133                          0.051        4.374        4.175
## 134                          0.070        4.365        4.090
## 135                          0.072        4.349        4.068
## 136                          0.077        4.258        3.956
## 137                          0.069        4.209        3.938
## 138                          0.077        4.001        3.698
## 139                          0.026        3.869        3.769
## 140                          0.107        3.985        3.565
## 141                          0.070        3.794        3.521
## 142                          0.071        3.762        3.485
## 143                          0.173        3.953        3.276
## 144                          0.092        3.781        3.419
## 145                          0.120        3.748        3.276
## 146                          0.074        3.611        3.322
## 147                          0.068        3.548        3.282
## 148                          0.058        3.259        3.030
## 149                          0.038        2.596        2.449
##     Logged.GDP.per.capita Social.support Healthy.life.expectancy
## 1                  10.775          0.954                  72.000
## 2                  10.933          0.954                  72.700
## 3                  11.117          0.942                  74.400
## 4                  10.878          0.983                  73.000
## 5                  10.932          0.942                  72.400
## 6                  11.053          0.954                  73.300
## 7                  10.867          0.934                  72.700
## 8                  11.647          0.908                  72.600
## 9                  10.643          0.948                  73.400
## 10                 10.906          0.934                  73.300
## 11                 10.796          0.940                  73.900
## 12                 10.575          0.939                  73.503
## 13                 10.873          0.903                  72.500
## 14                 10.776          0.926                  73.800
## 15                 11.342          0.947                  72.400
## 16                  9.880          0.891                  71.400
## 17                 10.707          0.934                  72.500
## 18                 10.556          0.947                  70.807
## 19                 11.023          0.920                  68.200
## 20                 10.823          0.906                  72.199
## 21                 10.704          0.942                  74.000
## 22                 10.669          0.862                  69.495
## 23                 10.674          0.931                  72.200
## 24                 10.871          0.898                  69.600
## 25                 11.085          0.844                  67.333
## 26                 10.743          0.891                  66.603
## 27                 10.571          0.932                  74.700
## 28                 10.623          0.880                  73.800
## 29                 10.529          0.948                  71.400
## 30                  9.053          0.813                  64.958
## 31                  9.966          0.925                  69.100
## 32                 11.488          0.915                  76.953
## 33                  9.318          0.821                  63.813
## 34                 10.369          0.936                  69.201
## 35                  9.577          0.882                  66.601
## 36                  9.859          0.831                  68.597
## 37                  9.186          0.877                  67.500
## 38                 10.499          0.935                  67.906
## 39                 10.576          0.802                  73.898
## 40                 10.481          0.941                  68.800
## 41                 10.350          0.896                  69.652
## 42                  8.836          0.918                  65.255
## 43                 10.071          0.882                  70.000
## 44                 10.382          0.898                  69.702
## 45                 10.155          0.952                  65.200
## 46                 10.284          0.832                  67.355
## 47                 10.817          0.843                  66.900
## 48                  9.787          0.873                  68.600
## 49                  9.054          0.762                  66.402
## 50                 10.008          0.905                  66.701
## 51                 10.315          0.927                  67.100
## 52                  9.557          0.847                  68.001
## 53                 10.358          0.943                  68.000
## 54                  9.805          0.888                  67.401
## 55                  8.620          0.864                  67.657
## 56                 10.611          0.884                  75.100
## 57                  9.962          0.898                  69.000
## 58                 10.421          0.879                  72.600
## 59                  8.648          0.812                  67.300
## 60                 10.217          0.924                  70.799
## 61                  9.076          0.830                  62.000
## 62                 10.651          0.799                  73.900
## 63                  9.458          0.832                  68.250
## 64                  9.590          0.870                  68.098
## 65                  9.454          0.857                  65.699
## 66                  9.313          0.821                  68.800
## 67                  8.538          0.893                  64.401
## 68                 10.279          0.823                  72.600
## 69                  9.046          0.810                  63.901
## 70                  9.400          0.935                  62.500
## 71                  9.448          0.893                  65.900
## 72                  9.940          0.858                  68.699
## 73                  9.802          0.853                  66.102
## 74                 10.576          0.820                  73.898
## 75                  9.853          0.910                  66.253
## 76                 10.189          0.903                  64.703
## 77                 11.000          0.836                  76.820
## 78                  8.091          0.860                  64.281
## 79                  8.973          0.850                  68.034
## 80                  9.622          0.827                  62.300
## 81                 10.238          0.817                  67.102
## 82                  9.365          0.811                  62.236
## 83                  8.117          0.636                  58.221
## 84                  9.673          0.811                  69.593
## 85                  8.551          0.644                  50.114
## 86                  9.487          0.799                  67.055
## 87                  8.120          0.774                  64.233
## 88                 10.016          0.931                  67.000
## 89                  9.826          0.913                  70.600
## 90                  9.569          0.836                  65.656
## 91                  8.189          0.710                  53.515
## 92                  8.118          0.710                  59.802
## 93                  9.520          0.697                  68.999
## 94                  9.693          0.805                  65.474
## 95                  8.580          0.727                  57.586
## 96                  7.098          0.641                  53.780
## 97                  9.629          0.983                  62.409
## 98                  7.686          0.690                  55.160
## 99                  8.087          0.489                  54.713
## 100                 8.947          0.728                  58.968
## 101                 8.454          0.693                  64.800
## 102                 7.838          0.639                  55.008
## 103                 9.403          0.860                  56.904
## 104                10.240          0.822                  67.199
## 105                 8.458          0.651                  58.709
## 106                 8.903          0.560                  66.208
## 107                 9.073          0.861                  66.700
## 108                 9.585          0.671                  64.300
## 109                 9.342          0.802                  66.005
## 110                 9.436          0.888                  64.902
## 111                 9.240          0.746                  60.583
## 112                 9.603          0.776                  59.962
## 113                 7.678          0.672                  54.151
## 114                 8.360          0.765                  62.000
## 115                 7.158          0.744                  54.706
## 116                 8.533          0.740                  50.102
## 117                 7.744          0.724                  51.969
## 118                 9.584          0.710                  66.300
## 119                 7.677          0.781                  56.101
## 120                 7.288          0.720                  56.498
## 121                 8.361          0.688                  60.704
## 122                 9.266          0.691                  67.201
## 123                 9.626          0.848                  67.355
## 124                 9.161          0.818                  56.799
## 125                 8.485          0.826                  62.250
## 126                 8.541          0.779                  59.302
## 127                 9.182          0.767                  67.000
## 128                 7.364          0.619                  48.478
## 129                 9.470          0.827                  67.299
## 130                 9.065          0.770                  50.833
## 131                 8.031          0.626                  57.349
## 132                 9.367          0.750                  61.998
## 133                 7.694          0.764                  59.000
## 134                 8.542          0.795                  57.161
## 135                 7.396          0.686                  59.305
## 136                 7.362          0.569                  54.914
## 137                 8.145          0.708                  55.809
## 138                 7.434          0.630                  51.651
## 139                 8.755          0.603                  60.633
## 140                 6.635          0.490                  53.400
## 141                 7.578          0.832                  57.122
## 142                 7.876          0.702                  57.999
## 143                 7.477          0.540                  55.700
## 144                 6.958          0.537                  57.948
## 145                 7.926          0.787                  48.700
## 146                 9.782          0.784                  59.269
## 147                 7.676          0.552                  61.400
## 148                 7.943          0.750                  56.201
## 149                 7.695          0.463                  52.493
##     Freedom.to.make.life.choices Generosity Perceptions.of.corruption
## 1                          0.949     -0.098                     0.186
## 2                          0.946      0.030                     0.179
## 3                          0.919      0.025                     0.292
## 4                          0.955      0.160                     0.673
## 5                          0.913      0.175                     0.338
## 6                          0.960      0.093                     0.270
## 7                          0.945      0.086                     0.237
## 8                          0.907     -0.034                     0.386
## 9                          0.929      0.134                     0.242
## 10                         0.908      0.042                     0.481
## 11                         0.914      0.159                     0.442
## 12                         0.800      0.031                     0.753
## 13                         0.875      0.011                     0.460
## 14                         0.915      0.089                     0.415
## 15                         0.879      0.077                     0.363
## 16                         0.934     -0.126                     0.809
## 17                         0.859      0.233                     0.459
## 18                         0.858     -0.208                     0.868
## 19                         0.837      0.098                     0.698
## 20                         0.783     -0.153                     0.646
## 21                         0.822     -0.147                     0.571
## 22                         0.925      0.089                     0.722
## 23                         0.927      0.133                     0.653
## 24                         0.784     -0.070                     0.721
## 25                         0.932      0.074                     0.589
## 26                         0.877     -0.149                     0.684
## 27                         0.761     -0.081                     0.745
## 28                         0.693     -0.084                     0.866
## 29                         0.949     -0.101                     0.806
## 30                         0.906     -0.038                     0.775
## 31                         0.896     -0.092                     0.590
## 32                         0.927     -0.018                     0.082
## 33                         0.869      0.257                     0.917
## 34                         0.766     -0.124                     0.911
## 35                         0.804     -0.071                     0.756
## 36                         0.862     -0.147                     0.799
## 37                         0.890     -0.137                     0.884
## 38                         0.773     -0.203                     0.826
## 39                         0.763     -0.015                     0.844
## 40                         0.909     -0.106                     0.527
## 41                         0.872     -0.166                     0.856
## 42                         0.970      0.311                     0.515
## 43                         0.742     -0.044                     0.830
## 44                         0.841     -0.165                     0.735
## 45                         0.853     -0.069                     0.733
## 46                         0.845     -0.219                     0.938
## 47                         0.867     -0.104                     0.736
## 48                         0.778      0.002                     0.835
## 49                         0.888     -0.110                     0.688
## 50                         0.867     -0.054                     0.789
## 51                         0.715     -0.162                     0.800
## 52                         0.837     -0.135                     0.841
## 53                         0.755     -0.186                     0.876
## 54                         0.884      0.287                     0.895
## 55                         0.836      0.020                     0.664
## 56                         0.796     -0.258                     0.638
## 57                         0.828     -0.182                     0.834
## 58                         0.892     -0.244                     0.887
## 59                         0.857      0.081                     0.809
## 60                         0.754     -0.118                     0.939
## 61                         0.917     -0.097                     0.742
## 62                         0.672     -0.083                     0.727
## 63                         0.822     -0.154                     0.891
## 64                         0.706      0.113                     0.931
## 65                         0.822     -0.079                     0.918
## 66                         0.842     -0.124                     0.843
## 67                         0.935      0.119                     0.908
## 68                         0.582     -0.288                     0.823
## 69                         0.875     -0.077                     0.839
## 70                         0.708      0.116                     0.856
## 71                         0.876      0.028                     0.882
## 72                         0.708     -0.034                     0.812
## 73                         0.860     -0.133                     0.714
## 74                         0.795      0.012                     0.626
## 75                         0.650     -0.180                     0.627
## 76                         0.718     -0.111                     0.845
## 77                         0.717      0.067                     0.403
## 78                         0.832     -0.056                     0.553
## 79                         0.940     -0.098                     0.796
## 80                         0.771     -0.087                     0.667
## 81                         0.895      0.125                     0.839
## 82                         0.873      0.542                     0.867
## 83                         0.695     -0.068                     0.745
## 84                         0.904     -0.146                     0.755
## 85                         0.741     -0.016                     0.794
## 86                         0.825     -0.168                     0.629
## 87                         0.782      0.152                     0.727
## 88                         0.788     -0.096                     0.932
## 89                         0.854      0.024                     0.825
## 90                         0.814     -0.223                     0.506
## 91                         0.731      0.026                     0.848
## 92                         0.695     -0.046                     0.801
## 93                         0.785     -0.030                     0.901
## 94                         0.751      0.038                     0.905
## 95                         0.807      0.123                     0.848
## 96                         0.806      0.018                     0.693
## 97                         0.877      0.273                     0.888
## 98                         0.697      0.424                     0.746
## 99                         0.757     -0.034                     0.661
## 100                        0.910      0.123                     0.658
## 101                        0.877     -0.041                     0.682
## 102                        0.697      0.095                     0.766
## 103                        0.749     -0.067                     0.860
## 104                        0.576     -0.139                     0.776
## 105                        0.726      0.098                     0.787
## 106                        0.774     -0.236                     0.801
## 107                        0.615     -0.169                     0.827
## 108                        0.783     -0.238                     0.655
## 109                        0.480     -0.067                     0.752
## 110                        0.724     -0.011                     0.924
## 111                        0.630     -0.053                     0.875
## 112                        0.731     -0.200                     0.840
## 113                        0.695     -0.009                     0.748
## 114                        0.959      0.034                     0.843
## 115                        0.882      0.061                     0.684
## 116                        0.737      0.037                     0.878
## 117                        0.697     -0.036                     0.827
## 118                        0.608      0.218                     0.714
## 119                        0.709      0.122                     0.855
## 120                        0.735      0.050                     0.850
## 121                        0.779      0.287                     0.825
## 122                        0.656     -0.201                     0.870
## 123                        0.525     -0.073                     0.898
## 124                        0.719     -0.149                     0.847
## 125                        0.653     -0.163                     0.821
## 126                        0.876      0.509                     0.660
## 127                        0.755     -0.167                     0.705
## 128                        0.579      0.041                     0.807
## 129                        0.841      0.079                     0.863
## 130                        0.647     -0.185                     0.708
## 131                        0.548      0.082                     0.781
## 132                        0.749     -0.182                     0.795
## 133                        0.752      0.082                     0.761
## 134                        0.561     -0.106                     0.731
## 135                        0.552     -0.005                     0.803
## 136                        0.619      0.032                     0.772
## 137                        0.782      0.061                     0.823
## 138                        0.717      0.084                     0.866
## 139                        0.893      0.089                     0.774
## 140                        0.626     -0.024                     0.607
## 141                        0.602     -0.147                     0.800
## 142                        0.833      0.183                     0.577
## 143                        0.593      0.422                     0.721
## 144                        0.780      0.038                     0.729
## 145                        0.715     -0.131                     0.915
## 146                        0.824     -0.246                     0.801
## 147                        0.897      0.061                     0.167
## 148                        0.677     -0.047                     0.821
## 149                        0.382     -0.102                     0.924
##     Ladder.score.in.Dystopia Explained.by..Log.GDP.per.capita
## 1                       2.43                            1.446
## 2                       2.43                            1.502
## 3                       2.43                            1.566
## 4                       2.43                            1.482
## 5                       2.43                            1.501
## 6                       2.43                            1.543
## 7                       2.43                            1.478
## 8                       2.43                            1.751
## 9                       2.43                            1.400
## 10                      2.43                            1.492
## 11                      2.43                            1.453
## 12                      2.43                            1.376
## 13                      2.43                            1.480
## 14                      2.43                            1.447
## 15                      2.43                            1.644
## 16                      2.43                            1.134
## 17                      2.43                            1.423
## 18                      2.43                            1.370
## 19                      2.43                            1.533
## 20                      2.43                            1.463
## 21                      2.43                            1.421
## 22                      2.43                            1.409
## 23                      2.43                            1.411
## 24                      2.43                            1.480
## 25                      2.43                            1.555
## 26                      2.43                            1.435
## 27                      2.43                            1.375
## 28                      2.43                            1.393
## 29                      2.43                            1.360
## 30                      2.43                            0.845
## 31                      2.43                            1.164
## 32                      2.43                            1.695
## 33                      2.43                            0.937
## 34                      2.43                            1.304
## 35                      2.43                            1.028
## 36                      2.43                            1.126
## 37                      2.43                            0.891
## 38                      2.43                            1.350
## 39                      2.43                            1.377
## 40                      2.43                            1.344
## 41                      2.43                            1.298
## 42                      2.43                            0.769
## 43                      2.43                            1.200
## 44                      2.43                            1.309
## 45                      2.43                            1.230
## 46                      2.43                            1.275
## 47                      2.43                            1.461
## 48                      2.43                            1.101
## 49                      2.43                            0.845
## 50                      2.43                            1.178
## 51                      2.43                            1.285
## 52                      2.43                            1.021
## 53                      2.43                            1.301
## 54                      2.43                            1.107
## 55                      2.43                            0.693
## 56                      2.43                            1.389
## 57                      2.43                            1.162
## 58                      2.43                            1.323
## 59                      2.43                            0.703
## 60                      2.43                            1.251
## 61                      2.43                            0.853
## 62                      2.43                            1.403
## 63                      2.43                            0.986
## 64                      2.43                            1.032
## 65                      2.43                            0.985
## 66                      2.43                            0.935
## 67                      2.43                            0.665
## 68                      2.43                            1.273
## 69                      2.43                            0.842
## 70                      2.43                            0.966
## 71                      2.43                            0.983
## 72                      2.43                            1.155
## 73                      2.43                            1.106
## 74                      2.43                            1.377
## 75                      2.43                            1.124
## 76                      2.43                            1.241
## 77                      2.43                            1.525
## 78                      2.43                            0.508
## 79                      2.43                            0.817
## 80                      2.43                            1.044
## 81                      2.43                            1.259
## 82                      2.43                            0.954
## 83                      2.43                            0.518
## 84                      2.43                            1.061
## 85                      2.43                            0.669
## 86                      2.43                            0.996
## 87                      2.43                            0.519
## 88                      2.43                            1.181
## 89                      2.43                            1.115
## 90                      2.43                            1.025
## 91                      2.43                            0.543
## 92                      2.43                            0.518
## 93                      2.43                            1.008
## 94                      2.43                            1.068
## 95                      2.43                            0.680
## 96                      2.43                            0.162
## 97                      2.43                            1.046
## 98                      2.43                            0.367
## 99                      2.43                            0.507
## 100                     2.43                            0.808
## 101                     2.43                            0.635
## 102                     2.43                            0.420
## 103                     2.43                            0.967
## 104                     2.43                            1.260
## 105                     2.43                            0.637
## 106                     2.43                            0.792
## 107                     2.43                            0.852
## 108                     2.43                            1.030
## 109                     2.43                            0.946
## 110                     2.43                            0.979
## 111                     2.43                            0.910
## 112                     2.43                            1.037
## 113                     2.43                            0.364
## 114                     2.43                            0.603
## 115                     2.43                            0.183
## 116                     2.43                            0.663
## 117                     2.43                            0.387
## 118                     2.43                            1.030
## 119                     2.43                            0.364
## 120                     2.43                            0.228
## 121                     2.43                            0.603
## 122                     2.43                            0.919
## 123                     2.43                            1.045
## 124                     2.43                            0.882
## 125                     2.43                            0.646
## 126                     2.43                            0.666
## 127                     2.43                            0.890
## 128                     2.43                            0.255
## 129                     2.43                            0.990
## 130                     2.43                            0.849
## 131                     2.43                            0.488
## 132                     2.43                            0.954
## 133                     2.43                            0.370
## 134                     2.43                            0.666
## 135                     2.43                            0.266
## 136                     2.43                            0.254
## 137                     2.43                            0.528
## 138                     2.43                            0.279
## 139                     2.43                            0.741
## 140                     2.43                            0.000
## 141                     2.43                            0.329
## 142                     2.43                            0.433
## 143                     2.43                            0.294
## 144                     2.43                            0.113
## 145                     2.43                            0.451
## 146                     2.43                            1.099
## 147                     2.43                            0.364
## 148                     2.43                            0.457
## 149                     2.43                            0.370
##     Explained.by..Social.support Explained.by..Healthy.life.expectancy
## 1                          1.106                                 0.741
## 2                          1.108                                 0.763
## 3                          1.079                                 0.816
## 4                          1.172                                 0.772
## 5                          1.079                                 0.753
## 6                          1.108                                 0.782
## 7                          1.062                                 0.763
## 8                          1.003                                 0.760
## 9                          1.094                                 0.785
## 10                         1.062                                 0.782
## 11                         1.076                                 0.801
## 12                         1.074                                 0.788
## 13                         0.993                                 0.757
## 14                         1.044                                 0.798
## 15                         1.092                                 0.753
## 16                         0.966                                 0.722
## 17                         1.062                                 0.757
## 18                         1.090                                 0.703
## 19                         1.030                                 0.621
## 20                         0.998                                 0.747
## 21                         1.081                                 0.804
## 22                         0.899                                 0.662
## 23                         1.055                                 0.747
## 24                         0.982                                 0.665
## 25                         0.860                                 0.594
## 26                         0.964                                 0.571
## 27                         1.057                                 0.826
## 28                         0.940                                 0.798
## 29                         1.093                                 0.722
## 30                         0.790                                 0.519
## 31                         1.042                                 0.649
## 32                         1.019                                 0.897
## 33                         0.807                                 0.483
## 34                         1.066                                 0.653
## 35                         0.944                                 0.571
## 36                         0.830                                 0.634
## 37                         0.932                                 0.599
## 38                         1.065                                 0.612
## 39                         0.765                                 0.801
## 40                         1.079                                 0.640
## 41                         0.976                                 0.667
## 42                         1.027                                 0.528
## 43                         0.946                                 0.678
## 44                         0.982                                 0.668
## 45                         1.103                                 0.527
## 46                         0.832                                 0.595
## 47                         0.857                                 0.580
## 48                         0.924                                 0.634
## 49                         0.675                                 0.565
## 50                         0.996                                 0.574
## 51                         1.047                                 0.587
## 52                         0.866                                 0.615
## 53                         1.083                                 0.615
## 54                         0.957                                 0.596
## 55                         0.904                                 0.604
## 56                         0.949                                 0.838
## 57                         0.980                                 0.646
## 58                         0.939                                 0.760
## 59                         0.787                                 0.593
## 60                         1.039                                 0.703
## 61                         0.828                                 0.426
## 62                         0.758                                 0.801
## 63                         0.833                                 0.623
## 64                         0.919                                 0.618
## 65                         0.888                                 0.542
## 66                         0.806                                 0.640
## 67                         0.971                                 0.501
## 68                         0.811                                 0.760
## 69                         0.782                                 0.486
## 70                         1.065                                 0.442
## 71                         0.970                                 0.549
## 72                         0.891                                 0.637
## 73                         0.879                                 0.555
## 74                         0.806                                 0.801
## 75                         1.007                                 0.560
## 76                         0.992                                 0.511
## 77                         0.841                                 0.893
## 78                         0.895                                 0.498
## 79                         0.873                                 0.616
## 80                         0.821                                 0.435
## 81                         0.797                                 0.587
## 82                         0.786                                 0.433
## 83                         0.392                                 0.307
## 84                         0.785                                 0.665
## 85                         0.409                                 0.052
## 86                         0.758                                 0.585
## 87                         0.702                                 0.496
## 88                         1.055                                 0.583
## 89                         1.015                                 0.697
## 90                         0.841                                 0.541
## 91                         0.556                                 0.159
## 92                         0.558                                 0.357
## 93                         0.529                                 0.646
## 94                         0.772                                 0.535
## 95                         0.595                                 0.287
## 96                         0.402                                 0.167
## 97                         1.172                                 0.439
## 98                         0.511                                 0.210
## 99                         0.058                                 0.196
## 100                        0.598                                 0.330
## 101                        0.520                                 0.514
## 102                        0.399                                 0.206
## 103                        0.895                                 0.265
## 104                        0.809                                 0.590
## 105                        0.423                                 0.322
## 106                        0.219                                 0.558
## 107                        0.897                                 0.574
## 108                        0.470                                 0.498
## 109                        0.765                                 0.552
## 110                        0.958                                 0.517
## 111                        0.638                                 0.381
## 112                        0.707                                 0.362
## 113                        0.472                                 0.179
## 114                        0.680                                 0.426
## 115                        0.634                                 0.196
## 116                        0.625                                 0.051
## 117                        0.590                                 0.110
## 118                        0.557                                 0.561
## 119                        0.718                                 0.240
## 120                        0.580                                 0.253
## 121                        0.508                                 0.385
## 122                        0.515                                 0.590
## 123                        0.868                                 0.595
## 124                        0.801                                 0.262
## 125                        0.819                                 0.434
## 126                        0.713                                 0.341
## 127                        0.685                                 0.583
## 128                        0.353                                 0.000
## 129                        0.820                                 0.593
## 130                        0.693                                 0.074
## 131                        0.367                                 0.279
## 132                        0.647                                 0.426
## 133                        0.679                                 0.331
## 134                        0.749                                 0.273
## 135                        0.503                                 0.341
## 136                        0.239                                 0.203
## 137                        0.552                                 0.231
## 138                        0.377                                 0.100
## 139                        0.316                                 0.383
## 140                        0.062                                 0.155
## 141                        0.831                                 0.272
## 142                        0.540                                 0.300
## 143                        0.173                                 0.227
## 144                        0.168                                 0.298
## 145                        0.731                                 0.007
## 146                        0.724                                 0.340
## 147                        0.202                                 0.407
## 148                        0.649                                 0.243
## 149                        0.000                                 0.126
##     Explained.by..Freedom.to.make.life.choices Explained.by..Generosity
## 1                                        0.691                    0.124
## 2                                        0.686                    0.208
## 3                                        0.653                    0.204
## 4                                        0.698                    0.293
## 5                                        0.647                    0.302
## 6                                        0.703                    0.249
## 7                                        0.685                    0.244
## 8                                        0.639                    0.166
## 9                                        0.665                    0.276
## 10                                       0.640                    0.215
## 11                                       0.647                    0.291
## 12                                       0.509                    0.208
## 13                                       0.600                    0.195
## 14                                       0.648                    0.246
## 15                                       0.606                    0.238
## 16                                       0.673                    0.105
## 17                                       0.580                    0.340
## 18                                       0.580                    0.052
## 19                                       0.554                    0.252
## 20                                       0.489                    0.088
## 21                                       0.536                    0.092
## 22                                       0.661                    0.246
## 23                                       0.664                    0.275
## 24                                       0.490                    0.142
## 25                                       0.670                    0.236
## 26                                       0.603                    0.090
## 27                                       0.462                    0.135
## 28                                       0.379                    0.133
## 29                                       0.690                    0.122
## 30                                       0.638                    0.163
## 31                                       0.625                    0.128
## 32                                       0.664                    0.176
## 33                                       0.593                    0.356
## 34                                       0.468                    0.107
## 35                                       0.514                    0.142
## 36                                       0.585                    0.092
## 37                                       0.618                    0.099
## 38                                       0.476                    0.056
## 39                                       0.464                    0.178
## 40                                       0.641                    0.119
## 41                                       0.596                    0.079
## 42                                       0.716                    0.391
## 43                                       0.438                    0.159
## 44                                       0.558                    0.080
## 45                                       0.573                    0.143
## 46                                       0.564                    0.045
## 47                                       0.591                    0.120
## 48                                       0.482                    0.189
## 49                                       0.615                    0.116
## 50                                       0.590                    0.153
## 51                                       0.405                    0.082
## 52                                       0.554                    0.100
## 53                                       0.454                    0.067
## 54                                       0.611                    0.375
## 55                                       0.553                    0.201
## 56                                       0.504                    0.020
## 57                                       0.544                    0.069
## 58                                       0.621                    0.029
## 59                                       0.578                    0.241
## 60                                       0.453                    0.111
## 61                                       0.651                    0.125
## 62                                       0.353                    0.134
## 63                                       0.536                    0.087
## 64                                       0.395                    0.261
## 65                                       0.536                    0.137
## 66                                       0.560                    0.107
## 67                                       0.673                    0.266
## 68                                       0.243                    0.000
## 69                                       0.600                    0.138
## 70                                       0.397                    0.263
## 71                                       0.602                    0.206
## 72                                       0.397                    0.166
## 73                                       0.581                    0.101
## 74                                       0.503                    0.196
## 75                                       0.326                    0.070
## 76                                       0.409                    0.115
## 77                                       0.408                    0.232
## 78                                       0.548                    0.152
## 79                                       0.679                    0.124
## 80                                       0.474                    0.131
## 81                                       0.624                    0.270
## 82                                       0.598                    0.541
## 83                                       0.381                    0.144
## 84                                       0.636                    0.093
## 85                                       0.438                    0.177
## 86                                       0.540                    0.079
## 87                                       0.488                    0.287
## 88                                       0.494                    0.125
## 89                                       0.575                    0.204
## 90                                       0.526                    0.043
## 91                                       0.425                    0.205
## 92                                       0.381                    0.158
## 93                                       0.491                    0.168
## 94                                       0.450                    0.212
## 95                                       0.517                    0.268
## 96                                       0.516                    0.200
## 97                                       0.602                    0.366
## 98                                       0.384                    0.465
## 99                                       0.457                    0.166
## 100                                      0.643                    0.268
## 101                                      0.603                    0.161
## 102                                      0.384                    0.250
## 103                                      0.447                    0.144
## 104                                      0.236                    0.097
## 105                                      0.418                    0.252
## 106                                      0.477                    0.034
## 107                                      0.284                    0.078
## 108                                      0.488                    0.032
## 109                                      0.119                    0.144
## 110                                      0.417                    0.181
## 111                                      0.302                    0.153
## 112                                      0.424                    0.058
## 113                                      0.381                    0.182
## 114                                      0.702                    0.210
## 115                                      0.608                    0.228
## 116                                      0.433                    0.212
## 117                                      0.384                    0.164
## 118                                      0.275                    0.330
## 119                                      0.398                    0.267
## 120                                      0.430                    0.221
## 121                                      0.483                    0.375
## 122                                      0.334                    0.057
## 123                                      0.175                    0.140
## 124                                      0.411                    0.091
## 125                                      0.330                    0.082
## 126                                      0.601                    0.520
## 127                                      0.455                    0.079
## 128                                      0.240                    0.215
## 129                                      0.559                    0.239
## 130                                      0.323                    0.067
## 131                                      0.202                    0.241
## 132                                      0.446                    0.069
## 133                                      0.451                    0.241
## 134                                      0.218                    0.119
## 135                                      0.207                    0.185
## 136                                      0.289                    0.209
## 137                                      0.487                    0.227
## 138                                      0.408                    0.243
## 139                                      0.622                    0.246
## 140                                      0.298                    0.172
## 141                                      0.268                    0.092
## 142                                      0.549                    0.307
## 143                                      0.257                    0.463
## 144                                      0.484                    0.213
## 145                                      0.405                    0.103
## 146                                      0.539                    0.027
## 147                                      0.627                    0.227
## 148                                      0.359                    0.157
## 149                                      0.000                    0.122
##     Explained.by..Perceptions.of.corruption Dystopia...residual
## 1                                     0.481               3.253
## 2                                     0.485               2.868
## 3                                     0.413               2.839
## 4                                     0.170               2.967
## 5                                     0.384               2.798
## 6                                     0.427               2.580
## 7                                     0.448               2.683
## 8                                     0.353               2.653
## 9                                     0.445               2.612
## 10                                    0.292               2.784
## 11                                    0.317               2.598
## 12                                    0.119               3.083
## 13                                    0.306               2.824
## 14                                    0.335               2.585
## 15                                    0.367               2.384
## 16                                    0.083               3.387
## 17                                    0.306               2.596
## 18                                    0.046               3.124
## 19                                    0.154               2.807
## 20                                    0.187               2.862
## 21                                    0.235               2.521
## 22                                    0.139               2.631
## 23                                    0.183               2.268
## 24                                    0.139               2.687
## 25                                    0.223               2.422
## 26                                    0.163               2.668
## 27                                    0.124               2.513
## 28                                    0.047               2.794
## 29                                    0.085               2.388
## 30                                    0.105               3.375
## 31                                    0.223               2.600
## 32                                    0.547               1.379
## 33                                    0.014               3.182
## 34                                    0.018               2.714
## 35                                    0.117               3.015
## 36                                    0.089               2.961
## 37                                    0.035               3.135
## 38                                    0.073               2.624
## 39                                    0.061               2.578
## 40                                    0.263               2.103
## 41                                    0.053               2.509
## 42                                    0.271               2.477
## 43                                    0.070               2.682
## 44                                    0.130               2.438
## 45                                    0.132               2.446
## 46                                    0.001               2.830
## 47                                    0.130               2.368
## 48                                    0.066               2.682
## 49                                    0.160               3.085
## 50                                    0.096               2.462
## 51                                    0.089               2.536
## 52                                    0.063               2.794
## 53                                    0.040               2.432
## 54                                    0.028               2.309
## 55                                    0.176               2.841
## 56                                    0.192               2.048
## 57                                    0.067               2.461
## 58                                    0.033               2.225
## 59                                    0.083               2.934
## 60                                    0.000               2.325
## 61                                    0.126               2.872
## 62                                    0.135               2.262
## 63                                    0.031               2.744
## 64                                    0.005               2.583
## 65                                    0.013               2.665
## 66                                    0.062               2.653
## 67                                    0.020               2.648
## 68                                    0.074               2.561
## 69                                    0.064               2.805
## 70                                    0.053               2.492
## 71                                    0.037               2.306
## 72                                    0.081               2.254
## 73                                    0.144               2.178
## 74                                    0.200               1.653
## 75                                    0.199               2.247
## 76                                    0.060               2.148
## 77                                    0.342               1.236
## 78                                    0.247               2.619
## 79                                    0.091               2.211
## 80                                    0.174               2.331
## 81                                    0.064               1.784
## 82                                    0.046               1.987
## 83                                    0.124               3.476
## 84                                    0.117               1.982
## 85                                    0.092               3.469
## 86                                    0.198               2.127
## 87                                    0.135               2.642
## 88                                    0.005               1.823
## 89                                    0.073               1.520
## 90                                    0.276               1.919
## 91                                    0.058               3.195
## 92                                    0.088               3.071
## 93                                    0.024               2.250
## 94                                    0.022               2.042
## 95                                    0.058               2.684
## 96                                    0.157               3.470
## 97                                    0.033               1.409
## 98                                    0.123               2.990
## 99                                    0.178               3.482
## 100                                   0.179               2.204
## 101                                   0.164               2.427
## 102                                   0.111               3.216
## 103                                   0.051               2.187
## 104                                   0.104               1.852
## 105                                   0.097               2.784
## 106                                   0.088               2.749
## 107                                   0.072               2.135
## 108                                   0.181               2.191
## 109                                   0.120               2.242
## 110                                   0.010               1.813
## 111                                   0.041               2.429
## 112                                   0.064               2.201
## 113                                   0.122               3.133
## 114                                   0.061               2.148
## 115                                   0.163               2.783
## 116                                   0.039               2.736
## 117                                   0.072               3.016
## 118                                   0.144               1.823
## 119                                   0.054               2.596
## 120                                   0.057               2.857
## 121                                   0.073               2.180
## 122                                   0.044               2.138
## 123                                   0.026               1.736
## 124                                   0.059               2.068
## 125                                   0.075               2.131
## 126                                   0.178               1.407
## 127                                   0.150               1.553
## 128                                   0.084               3.209
## 129                                   0.049               1.075
## 130                                   0.147               2.155
## 131                                   0.101               2.610
## 132                                   0.092               1.648
## 133                                   0.114               2.089
## 134                                   0.133               2.069
## 135                                   0.087               2.620
## 136                                   0.107               2.806
## 137                                   0.074               1.975
## 138                                   0.047               2.396
## 139                                   0.106               1.405
## 140                                   0.212               2.876
## 141                                   0.089               1.776
## 142                                   0.231               1.263
## 143                                   0.139               2.060
## 144                                   0.134               2.190
## 145                                   0.015               1.800
## 146                                   0.088               0.648
## 147                                   0.493               1.095
## 148                                   0.075               1.205
## 149                                   0.010               1.895
```

#Clean Up Data

```r
happy <- janitor::clean_names(happy)
happy
```

```
##                  country_name                 regional_indicator ladder_score
## 1                     Finland                     Western Europe        7.842
## 2                     Denmark                     Western Europe        7.620
## 3                 Switzerland                     Western Europe        7.571
## 4                     Iceland                     Western Europe        7.554
## 5                 Netherlands                     Western Europe        7.464
## 6                      Norway                     Western Europe        7.392
## 7                      Sweden                     Western Europe        7.363
## 8                  Luxembourg                     Western Europe        7.324
## 9                 New Zealand              North America and ANZ        7.277
## 10                    Austria                     Western Europe        7.268
## 11                  Australia              North America and ANZ        7.183
## 12                     Israel       Middle East and North Africa        7.157
## 13                    Germany                     Western Europe        7.155
## 14                     Canada              North America and ANZ        7.103
## 15                    Ireland                     Western Europe        7.085
## 16                 Costa Rica        Latin America and Caribbean        7.069
## 17             United Kingdom                     Western Europe        7.064
## 18             Czech Republic         Central and Eastern Europe        6.965
## 19              United States              North America and ANZ        6.951
## 20                    Belgium                     Western Europe        6.834
## 21                     France                     Western Europe        6.690
## 22                    Bahrain       Middle East and North Africa        6.647
## 23                      Malta                     Western Europe        6.602
## 24   Taiwan Province of China                          East Asia        6.584
## 25       United Arab Emirates       Middle East and North Africa        6.561
## 26               Saudi Arabia       Middle East and North Africa        6.494
## 27                      Spain                     Western Europe        6.491
## 28                      Italy                     Western Europe        6.483
## 29                   Slovenia         Central and Eastern Europe        6.461
## 30                  Guatemala        Latin America and Caribbean        6.435
## 31                    Uruguay        Latin America and Caribbean        6.431
## 32                  Singapore                     Southeast Asia        6.377
## 33                     Kosovo         Central and Eastern Europe        6.372
## 34                   Slovakia         Central and Eastern Europe        6.331
## 35                     Brazil        Latin America and Caribbean        6.330
## 36                     Mexico        Latin America and Caribbean        6.317
## 37                    Jamaica        Latin America and Caribbean        6.309
## 38                  Lithuania         Central and Eastern Europe        6.255
## 39                     Cyprus                     Western Europe        6.223
## 40                    Estonia         Central and Eastern Europe        6.189
## 41                     Panama        Latin America and Caribbean        6.180
## 42                 Uzbekistan Commonwealth of Independent States        6.179
## 43                      Chile        Latin America and Caribbean        6.172
## 44                     Poland         Central and Eastern Europe        6.166
## 45                 Kazakhstan Commonwealth of Independent States        6.152
## 46                    Romania         Central and Eastern Europe        6.140
## 47                     Kuwait       Middle East and North Africa        6.106
## 48                     Serbia         Central and Eastern Europe        6.078
## 49                El Salvador        Latin America and Caribbean        6.061
## 50                  Mauritius                 Sub-Saharan Africa        6.049
## 51                     Latvia         Central and Eastern Europe        6.032
## 52                   Colombia        Latin America and Caribbean        6.012
## 53                    Hungary         Central and Eastern Europe        5.992
## 54                   Thailand                     Southeast Asia        5.985
## 55                  Nicaragua        Latin America and Caribbean        5.972
## 56                      Japan                          East Asia        5.940
## 57                  Argentina        Latin America and Caribbean        5.929
## 58                   Portugal                     Western Europe        5.929
## 59                   Honduras        Latin America and Caribbean        5.919
## 60                    Croatia         Central and Eastern Europe        5.882
## 61                Philippines                     Southeast Asia        5.880
## 62                South Korea                          East Asia        5.845
## 63                       Peru        Latin America and Caribbean        5.840
## 64     Bosnia and Herzegovina         Central and Eastern Europe        5.813
## 65                    Moldova Commonwealth of Independent States        5.766
## 66                    Ecuador        Latin America and Caribbean        5.764
## 67                 Kyrgyzstan Commonwealth of Independent States        5.744
## 68                     Greece                     Western Europe        5.723
## 69                    Bolivia        Latin America and Caribbean        5.716
## 70                   Mongolia                          East Asia        5.677
## 71                   Paraguay        Latin America and Caribbean        5.653
## 72                 Montenegro         Central and Eastern Europe        5.581
## 73         Dominican Republic        Latin America and Caribbean        5.545
## 74               North Cyprus                     Western Europe        5.536
## 75                    Belarus Commonwealth of Independent States        5.534
## 76                     Russia Commonwealth of Independent States        5.477
## 77  Hong Kong S.A.R. of China                          East Asia        5.477
## 78                 Tajikistan Commonwealth of Independent States        5.466
## 79                    Vietnam                     Southeast Asia        5.411
## 80                      Libya       Middle East and North Africa        5.410
## 81                   Malaysia                     Southeast Asia        5.384
## 82                  Indonesia                     Southeast Asia        5.345
## 83        Congo (Brazzaville)                 Sub-Saharan Africa        5.342
## 84                      China                          East Asia        5.339
## 85                Ivory Coast                 Sub-Saharan Africa        5.306
## 86                    Armenia Commonwealth of Independent States        5.283
## 87                      Nepal                         South Asia        5.269
## 88                   Bulgaria         Central and Eastern Europe        5.266
## 89                   Maldives                         South Asia        5.198
## 90                 Azerbaijan Commonwealth of Independent States        5.171
## 91                   Cameroon                 Sub-Saharan Africa        5.142
## 92                    Senegal                 Sub-Saharan Africa        5.132
## 93                    Albania         Central and Eastern Europe        5.117
## 94            North Macedonia         Central and Eastern Europe        5.101
## 95                      Ghana                 Sub-Saharan Africa        5.088
## 96                      Niger                 Sub-Saharan Africa        5.074
## 97               Turkmenistan Commonwealth of Independent States        5.066
## 98                     Gambia                 Sub-Saharan Africa        5.051
## 99                      Benin                 Sub-Saharan Africa        5.045
## 100                      Laos                     Southeast Asia        5.030
## 101                Bangladesh                         South Asia        5.025
## 102                    Guinea                 Sub-Saharan Africa        4.984
## 103              South Africa                 Sub-Saharan Africa        4.956
## 104                    Turkey       Middle East and North Africa        4.948
## 105                  Pakistan                         South Asia        4.934
## 106                   Morocco       Middle East and North Africa        4.918
## 107                 Venezuela        Latin America and Caribbean        4.892
## 108                   Georgia Commonwealth of Independent States        4.891
## 109                   Algeria       Middle East and North Africa        4.887
## 110                   Ukraine Commonwealth of Independent States        4.875
## 111                      Iraq       Middle East and North Africa        4.854
## 112                     Gabon                 Sub-Saharan Africa        4.852
## 113              Burkina Faso                 Sub-Saharan Africa        4.834
## 114                  Cambodia                     Southeast Asia        4.830
## 115                Mozambique                 Sub-Saharan Africa        4.794
## 116                   Nigeria                 Sub-Saharan Africa        4.759
## 117                      Mali                 Sub-Saharan Africa        4.723
## 118                      Iran       Middle East and North Africa        4.721
## 119                    Uganda                 Sub-Saharan Africa        4.636
## 120                   Liberia                 Sub-Saharan Africa        4.625
## 121                     Kenya                 Sub-Saharan Africa        4.607
## 122                   Tunisia       Middle East and North Africa        4.596
## 123                   Lebanon       Middle East and North Africa        4.584
## 124                   Namibia                 Sub-Saharan Africa        4.574
## 125   Palestinian Territories       Middle East and North Africa        4.517
## 126                   Myanmar                     Southeast Asia        4.426
## 127                    Jordan       Middle East and North Africa        4.395
## 128                      Chad                 Sub-Saharan Africa        4.355
## 129                 Sri Lanka                         South Asia        4.325
## 130                 Swaziland                 Sub-Saharan Africa        4.308
## 131                   Comoros                 Sub-Saharan Africa        4.289
## 132                     Egypt       Middle East and North Africa        4.283
## 133                  Ethiopia                 Sub-Saharan Africa        4.275
## 134                Mauritania                 Sub-Saharan Africa        4.227
## 135                Madagascar                 Sub-Saharan Africa        4.208
## 136                      Togo                 Sub-Saharan Africa        4.107
## 137                    Zambia                 Sub-Saharan Africa        4.073
## 138              Sierra Leone                 Sub-Saharan Africa        3.849
## 139                     India                         South Asia        3.819
## 140                   Burundi                 Sub-Saharan Africa        3.775
## 141                     Yemen       Middle East and North Africa        3.658
## 142                  Tanzania                 Sub-Saharan Africa        3.623
## 143                     Haiti        Latin America and Caribbean        3.615
## 144                    Malawi                 Sub-Saharan Africa        3.600
## 145                   Lesotho                 Sub-Saharan Africa        3.512
## 146                  Botswana                 Sub-Saharan Africa        3.467
## 147                    Rwanda                 Sub-Saharan Africa        3.415
## 148                  Zimbabwe                 Sub-Saharan Africa        3.145
## 149               Afghanistan                         South Asia        2.523
##     standard_error_of_ladder_score upperwhisker lowerwhisker
## 1                            0.032        7.904        7.780
## 2                            0.035        7.687        7.552
## 3                            0.036        7.643        7.500
## 4                            0.059        7.670        7.438
## 5                            0.027        7.518        7.410
## 6                            0.035        7.462        7.323
## 7                            0.036        7.433        7.293
## 8                            0.037        7.396        7.252
## 9                            0.040        7.355        7.198
## 10                           0.036        7.337        7.198
## 11                           0.041        7.265        7.102
## 12                           0.034        7.224        7.090
## 13                           0.040        7.232        7.077
## 14                           0.042        7.185        7.021
## 15                           0.040        7.164        7.006
## 16                           0.056        7.179        6.960
## 17                           0.038        7.138        6.990
## 18                           0.049        7.062        6.868
## 19                           0.049        7.047        6.856
## 20                           0.034        6.901        6.767
## 21                           0.037        6.762        6.618
## 22                           0.068        6.779        6.514
## 23                           0.044        6.688        6.516
## 24                           0.038        6.659        6.510
## 25                           0.039        6.637        6.484
## 26                           0.056        6.604        6.384
## 27                           0.042        6.574        6.408
## 28                           0.045        6.572        6.395
## 29                           0.043        6.546        6.376
## 30                           0.073        6.577        6.292
## 31                           0.046        6.521        6.341
## 32                           0.043        6.460        6.293
## 33                           0.059        6.487        6.257
## 34                           0.041        6.411        6.251
## 35                           0.043        6.415        6.245
## 36                           0.053        6.420        6.213
## 37                           0.156        6.615        6.004
## 38                           0.045        6.344        6.167
## 39                           0.049        6.319        6.128
## 40                           0.038        6.263        6.115
## 41                           0.073        6.323        6.036
## 42                           0.068        6.312        6.045
## 43                           0.046        6.262        6.081
## 44                           0.040        6.245        6.087
## 45                           0.047        6.243        6.060
## 46                           0.057        6.253        6.027
## 47                           0.066        6.235        5.977
## 48                           0.053        6.181        5.974
## 49                           0.065        6.188        5.933
## 50                           0.059        6.165        5.933
## 51                           0.036        6.103        5.961
## 52                           0.061        6.132        5.892
## 53                           0.047        6.085        5.899
## 54                           0.047        6.077        5.893
## 55                           0.083        6.134        5.810
## 56                           0.040        6.020        5.861
## 57                           0.056        6.040        5.819
## 58                           0.055        6.037        5.821
## 59                           0.082        6.081        5.758
## 60                           0.048        5.975        5.788
## 61                           0.052        5.982        5.778
## 62                           0.042        5.928        5.763
## 63                           0.075        5.988        5.692
## 64                           0.050        5.911        5.715
## 65                           0.046        5.856        5.677
## 66                           0.057        5.875        5.653
## 67                           0.046        5.834        5.653
## 68                           0.046        5.813        5.632
## 69                           0.053        5.819        5.613
## 70                           0.042        5.760        5.595
## 71                           0.092        5.832        5.473
## 72                           0.054        5.686        5.475
## 73                           0.071        5.685        5.405
## 74                           0.051        5.636        5.435
## 75                           0.047        5.625        5.442
## 76                           0.033        5.541        5.413
## 77                           0.049        5.573        5.380
## 78                           0.034        5.532        5.400
## 79                           0.039        5.488        5.334
## 80                           0.076        5.558        5.262
## 81                           0.049        5.480        5.289
## 82                           0.056        5.454        5.235
## 83                           0.097        5.533        5.151
## 84                           0.029        5.397        5.281
## 85                           0.078        5.460        5.152
## 86                           0.058        5.397        5.168
## 87                           0.070        5.406        5.132
## 88                           0.054        5.371        5.160
## 89                           0.072        5.339        5.057
## 90                           0.040        5.250        5.091
## 91                           0.074        5.288        4.996
## 92                           0.068        5.266        4.998
## 93                           0.059        5.234        5.001
## 94                           0.051        5.202        5.001
## 95                           0.067        5.219        4.958
## 96                           0.102        5.273        4.875
## 97                           0.036        5.136        4.996
## 98                           0.089        5.225        4.877
## 99                           0.073        5.189        4.901
## 100                          0.045        5.119        4.941
## 101                          0.046        5.115        4.934
## 102                          0.090        5.160        4.808
## 103                          0.060        5.074        4.839
## 104                          0.046        5.038        4.857
## 105                          0.068        5.066        4.802
## 106                          0.060        5.036        4.800
## 107                          0.064        5.017        4.767
## 108                          0.054        4.998        4.785
## 109                          0.053        4.991        4.783
## 110                          0.052        4.977        4.773
## 111                          0.059        4.970        4.738
## 112                          0.075        4.998        4.706
## 113                          0.081        4.993        4.675
## 114                          0.067        4.963        4.698
## 115                          0.103        4.997        4.592
## 116                          0.052        4.861        4.658
## 117                          0.082        4.884        4.563
## 118                          0.055        4.828        4.614
## 119                          0.073        4.780        4.493
## 120                          0.106        4.833        4.417
## 121                          0.072        4.747        4.466
## 122                          0.058        4.709        4.484
## 123                          0.055        4.691        4.477
## 124                          0.064        4.700        4.448
## 125                          0.067        4.649        4.384
## 126                          0.052        4.527        4.324
## 127                          0.062        4.516        4.273
## 128                          0.094        4.540        4.171
## 129                          0.066        4.454        4.196
## 130                          0.071        4.448        4.168
## 131                          0.084        4.454        4.123
## 132                          0.045        4.371        4.195
## 133                          0.051        4.374        4.175
## 134                          0.070        4.365        4.090
## 135                          0.072        4.349        4.068
## 136                          0.077        4.258        3.956
## 137                          0.069        4.209        3.938
## 138                          0.077        4.001        3.698
## 139                          0.026        3.869        3.769
## 140                          0.107        3.985        3.565
## 141                          0.070        3.794        3.521
## 142                          0.071        3.762        3.485
## 143                          0.173        3.953        3.276
## 144                          0.092        3.781        3.419
## 145                          0.120        3.748        3.276
## 146                          0.074        3.611        3.322
## 147                          0.068        3.548        3.282
## 148                          0.058        3.259        3.030
## 149                          0.038        2.596        2.449
##     logged_gdp_per_capita social_support healthy_life_expectancy
## 1                  10.775          0.954                  72.000
## 2                  10.933          0.954                  72.700
## 3                  11.117          0.942                  74.400
## 4                  10.878          0.983                  73.000
## 5                  10.932          0.942                  72.400
## 6                  11.053          0.954                  73.300
## 7                  10.867          0.934                  72.700
## 8                  11.647          0.908                  72.600
## 9                  10.643          0.948                  73.400
## 10                 10.906          0.934                  73.300
## 11                 10.796          0.940                  73.900
## 12                 10.575          0.939                  73.503
## 13                 10.873          0.903                  72.500
## 14                 10.776          0.926                  73.800
## 15                 11.342          0.947                  72.400
## 16                  9.880          0.891                  71.400
## 17                 10.707          0.934                  72.500
## 18                 10.556          0.947                  70.807
## 19                 11.023          0.920                  68.200
## 20                 10.823          0.906                  72.199
## 21                 10.704          0.942                  74.000
## 22                 10.669          0.862                  69.495
## 23                 10.674          0.931                  72.200
## 24                 10.871          0.898                  69.600
## 25                 11.085          0.844                  67.333
## 26                 10.743          0.891                  66.603
## 27                 10.571          0.932                  74.700
## 28                 10.623          0.880                  73.800
## 29                 10.529          0.948                  71.400
## 30                  9.053          0.813                  64.958
## 31                  9.966          0.925                  69.100
## 32                 11.488          0.915                  76.953
## 33                  9.318          0.821                  63.813
## 34                 10.369          0.936                  69.201
## 35                  9.577          0.882                  66.601
## 36                  9.859          0.831                  68.597
## 37                  9.186          0.877                  67.500
## 38                 10.499          0.935                  67.906
## 39                 10.576          0.802                  73.898
## 40                 10.481          0.941                  68.800
## 41                 10.350          0.896                  69.652
## 42                  8.836          0.918                  65.255
## 43                 10.071          0.882                  70.000
## 44                 10.382          0.898                  69.702
## 45                 10.155          0.952                  65.200
## 46                 10.284          0.832                  67.355
## 47                 10.817          0.843                  66.900
## 48                  9.787          0.873                  68.600
## 49                  9.054          0.762                  66.402
## 50                 10.008          0.905                  66.701
## 51                 10.315          0.927                  67.100
## 52                  9.557          0.847                  68.001
## 53                 10.358          0.943                  68.000
## 54                  9.805          0.888                  67.401
## 55                  8.620          0.864                  67.657
## 56                 10.611          0.884                  75.100
## 57                  9.962          0.898                  69.000
## 58                 10.421          0.879                  72.600
## 59                  8.648          0.812                  67.300
## 60                 10.217          0.924                  70.799
## 61                  9.076          0.830                  62.000
## 62                 10.651          0.799                  73.900
## 63                  9.458          0.832                  68.250
## 64                  9.590          0.870                  68.098
## 65                  9.454          0.857                  65.699
## 66                  9.313          0.821                  68.800
## 67                  8.538          0.893                  64.401
## 68                 10.279          0.823                  72.600
## 69                  9.046          0.810                  63.901
## 70                  9.400          0.935                  62.500
## 71                  9.448          0.893                  65.900
## 72                  9.940          0.858                  68.699
## 73                  9.802          0.853                  66.102
## 74                 10.576          0.820                  73.898
## 75                  9.853          0.910                  66.253
## 76                 10.189          0.903                  64.703
## 77                 11.000          0.836                  76.820
## 78                  8.091          0.860                  64.281
## 79                  8.973          0.850                  68.034
## 80                  9.622          0.827                  62.300
## 81                 10.238          0.817                  67.102
## 82                  9.365          0.811                  62.236
## 83                  8.117          0.636                  58.221
## 84                  9.673          0.811                  69.593
## 85                  8.551          0.644                  50.114
## 86                  9.487          0.799                  67.055
## 87                  8.120          0.774                  64.233
## 88                 10.016          0.931                  67.000
## 89                  9.826          0.913                  70.600
## 90                  9.569          0.836                  65.656
## 91                  8.189          0.710                  53.515
## 92                  8.118          0.710                  59.802
## 93                  9.520          0.697                  68.999
## 94                  9.693          0.805                  65.474
## 95                  8.580          0.727                  57.586
## 96                  7.098          0.641                  53.780
## 97                  9.629          0.983                  62.409
## 98                  7.686          0.690                  55.160
## 99                  8.087          0.489                  54.713
## 100                 8.947          0.728                  58.968
## 101                 8.454          0.693                  64.800
## 102                 7.838          0.639                  55.008
## 103                 9.403          0.860                  56.904
## 104                10.240          0.822                  67.199
## 105                 8.458          0.651                  58.709
## 106                 8.903          0.560                  66.208
## 107                 9.073          0.861                  66.700
## 108                 9.585          0.671                  64.300
## 109                 9.342          0.802                  66.005
## 110                 9.436          0.888                  64.902
## 111                 9.240          0.746                  60.583
## 112                 9.603          0.776                  59.962
## 113                 7.678          0.672                  54.151
## 114                 8.360          0.765                  62.000
## 115                 7.158          0.744                  54.706
## 116                 8.533          0.740                  50.102
## 117                 7.744          0.724                  51.969
## 118                 9.584          0.710                  66.300
## 119                 7.677          0.781                  56.101
## 120                 7.288          0.720                  56.498
## 121                 8.361          0.688                  60.704
## 122                 9.266          0.691                  67.201
## 123                 9.626          0.848                  67.355
## 124                 9.161          0.818                  56.799
## 125                 8.485          0.826                  62.250
## 126                 8.541          0.779                  59.302
## 127                 9.182          0.767                  67.000
## 128                 7.364          0.619                  48.478
## 129                 9.470          0.827                  67.299
## 130                 9.065          0.770                  50.833
## 131                 8.031          0.626                  57.349
## 132                 9.367          0.750                  61.998
## 133                 7.694          0.764                  59.000
## 134                 8.542          0.795                  57.161
## 135                 7.396          0.686                  59.305
## 136                 7.362          0.569                  54.914
## 137                 8.145          0.708                  55.809
## 138                 7.434          0.630                  51.651
## 139                 8.755          0.603                  60.633
## 140                 6.635          0.490                  53.400
## 141                 7.578          0.832                  57.122
## 142                 7.876          0.702                  57.999
## 143                 7.477          0.540                  55.700
## 144                 6.958          0.537                  57.948
## 145                 7.926          0.787                  48.700
## 146                 9.782          0.784                  59.269
## 147                 7.676          0.552                  61.400
## 148                 7.943          0.750                  56.201
## 149                 7.695          0.463                  52.493
##     freedom_to_make_life_choices generosity perceptions_of_corruption
## 1                          0.949     -0.098                     0.186
## 2                          0.946      0.030                     0.179
## 3                          0.919      0.025                     0.292
## 4                          0.955      0.160                     0.673
## 5                          0.913      0.175                     0.338
## 6                          0.960      0.093                     0.270
## 7                          0.945      0.086                     0.237
## 8                          0.907     -0.034                     0.386
## 9                          0.929      0.134                     0.242
## 10                         0.908      0.042                     0.481
## 11                         0.914      0.159                     0.442
## 12                         0.800      0.031                     0.753
## 13                         0.875      0.011                     0.460
## 14                         0.915      0.089                     0.415
## 15                         0.879      0.077                     0.363
## 16                         0.934     -0.126                     0.809
## 17                         0.859      0.233                     0.459
## 18                         0.858     -0.208                     0.868
## 19                         0.837      0.098                     0.698
## 20                         0.783     -0.153                     0.646
## 21                         0.822     -0.147                     0.571
## 22                         0.925      0.089                     0.722
## 23                         0.927      0.133                     0.653
## 24                         0.784     -0.070                     0.721
## 25                         0.932      0.074                     0.589
## 26                         0.877     -0.149                     0.684
## 27                         0.761     -0.081                     0.745
## 28                         0.693     -0.084                     0.866
## 29                         0.949     -0.101                     0.806
## 30                         0.906     -0.038                     0.775
## 31                         0.896     -0.092                     0.590
## 32                         0.927     -0.018                     0.082
## 33                         0.869      0.257                     0.917
## 34                         0.766     -0.124                     0.911
## 35                         0.804     -0.071                     0.756
## 36                         0.862     -0.147                     0.799
## 37                         0.890     -0.137                     0.884
## 38                         0.773     -0.203                     0.826
## 39                         0.763     -0.015                     0.844
## 40                         0.909     -0.106                     0.527
## 41                         0.872     -0.166                     0.856
## 42                         0.970      0.311                     0.515
## 43                         0.742     -0.044                     0.830
## 44                         0.841     -0.165                     0.735
## 45                         0.853     -0.069                     0.733
## 46                         0.845     -0.219                     0.938
## 47                         0.867     -0.104                     0.736
## 48                         0.778      0.002                     0.835
## 49                         0.888     -0.110                     0.688
## 50                         0.867     -0.054                     0.789
## 51                         0.715     -0.162                     0.800
## 52                         0.837     -0.135                     0.841
## 53                         0.755     -0.186                     0.876
## 54                         0.884      0.287                     0.895
## 55                         0.836      0.020                     0.664
## 56                         0.796     -0.258                     0.638
## 57                         0.828     -0.182                     0.834
## 58                         0.892     -0.244                     0.887
## 59                         0.857      0.081                     0.809
## 60                         0.754     -0.118                     0.939
## 61                         0.917     -0.097                     0.742
## 62                         0.672     -0.083                     0.727
## 63                         0.822     -0.154                     0.891
## 64                         0.706      0.113                     0.931
## 65                         0.822     -0.079                     0.918
## 66                         0.842     -0.124                     0.843
## 67                         0.935      0.119                     0.908
## 68                         0.582     -0.288                     0.823
## 69                         0.875     -0.077                     0.839
## 70                         0.708      0.116                     0.856
## 71                         0.876      0.028                     0.882
## 72                         0.708     -0.034                     0.812
## 73                         0.860     -0.133                     0.714
## 74                         0.795      0.012                     0.626
## 75                         0.650     -0.180                     0.627
## 76                         0.718     -0.111                     0.845
## 77                         0.717      0.067                     0.403
## 78                         0.832     -0.056                     0.553
## 79                         0.940     -0.098                     0.796
## 80                         0.771     -0.087                     0.667
## 81                         0.895      0.125                     0.839
## 82                         0.873      0.542                     0.867
## 83                         0.695     -0.068                     0.745
## 84                         0.904     -0.146                     0.755
## 85                         0.741     -0.016                     0.794
## 86                         0.825     -0.168                     0.629
## 87                         0.782      0.152                     0.727
## 88                         0.788     -0.096                     0.932
## 89                         0.854      0.024                     0.825
## 90                         0.814     -0.223                     0.506
## 91                         0.731      0.026                     0.848
## 92                         0.695     -0.046                     0.801
## 93                         0.785     -0.030                     0.901
## 94                         0.751      0.038                     0.905
## 95                         0.807      0.123                     0.848
## 96                         0.806      0.018                     0.693
## 97                         0.877      0.273                     0.888
## 98                         0.697      0.424                     0.746
## 99                         0.757     -0.034                     0.661
## 100                        0.910      0.123                     0.658
## 101                        0.877     -0.041                     0.682
## 102                        0.697      0.095                     0.766
## 103                        0.749     -0.067                     0.860
## 104                        0.576     -0.139                     0.776
## 105                        0.726      0.098                     0.787
## 106                        0.774     -0.236                     0.801
## 107                        0.615     -0.169                     0.827
## 108                        0.783     -0.238                     0.655
## 109                        0.480     -0.067                     0.752
## 110                        0.724     -0.011                     0.924
## 111                        0.630     -0.053                     0.875
## 112                        0.731     -0.200                     0.840
## 113                        0.695     -0.009                     0.748
## 114                        0.959      0.034                     0.843
## 115                        0.882      0.061                     0.684
## 116                        0.737      0.037                     0.878
## 117                        0.697     -0.036                     0.827
## 118                        0.608      0.218                     0.714
## 119                        0.709      0.122                     0.855
## 120                        0.735      0.050                     0.850
## 121                        0.779      0.287                     0.825
## 122                        0.656     -0.201                     0.870
## 123                        0.525     -0.073                     0.898
## 124                        0.719     -0.149                     0.847
## 125                        0.653     -0.163                     0.821
## 126                        0.876      0.509                     0.660
## 127                        0.755     -0.167                     0.705
## 128                        0.579      0.041                     0.807
## 129                        0.841      0.079                     0.863
## 130                        0.647     -0.185                     0.708
## 131                        0.548      0.082                     0.781
## 132                        0.749     -0.182                     0.795
## 133                        0.752      0.082                     0.761
## 134                        0.561     -0.106                     0.731
## 135                        0.552     -0.005                     0.803
## 136                        0.619      0.032                     0.772
## 137                        0.782      0.061                     0.823
## 138                        0.717      0.084                     0.866
## 139                        0.893      0.089                     0.774
## 140                        0.626     -0.024                     0.607
## 141                        0.602     -0.147                     0.800
## 142                        0.833      0.183                     0.577
## 143                        0.593      0.422                     0.721
## 144                        0.780      0.038                     0.729
## 145                        0.715     -0.131                     0.915
## 146                        0.824     -0.246                     0.801
## 147                        0.897      0.061                     0.167
## 148                        0.677     -0.047                     0.821
## 149                        0.382     -0.102                     0.924
##     ladder_score_in_dystopia explained_by_log_gdp_per_capita
## 1                       2.43                           1.446
## 2                       2.43                           1.502
## 3                       2.43                           1.566
## 4                       2.43                           1.482
## 5                       2.43                           1.501
## 6                       2.43                           1.543
## 7                       2.43                           1.478
## 8                       2.43                           1.751
## 9                       2.43                           1.400
## 10                      2.43                           1.492
## 11                      2.43                           1.453
## 12                      2.43                           1.376
## 13                      2.43                           1.480
## 14                      2.43                           1.447
## 15                      2.43                           1.644
## 16                      2.43                           1.134
## 17                      2.43                           1.423
## 18                      2.43                           1.370
## 19                      2.43                           1.533
## 20                      2.43                           1.463
## 21                      2.43                           1.421
## 22                      2.43                           1.409
## 23                      2.43                           1.411
## 24                      2.43                           1.480
## 25                      2.43                           1.555
## 26                      2.43                           1.435
## 27                      2.43                           1.375
## 28                      2.43                           1.393
## 29                      2.43                           1.360
## 30                      2.43                           0.845
## 31                      2.43                           1.164
## 32                      2.43                           1.695
## 33                      2.43                           0.937
## 34                      2.43                           1.304
## 35                      2.43                           1.028
## 36                      2.43                           1.126
## 37                      2.43                           0.891
## 38                      2.43                           1.350
## 39                      2.43                           1.377
## 40                      2.43                           1.344
## 41                      2.43                           1.298
## 42                      2.43                           0.769
## 43                      2.43                           1.200
## 44                      2.43                           1.309
## 45                      2.43                           1.230
## 46                      2.43                           1.275
## 47                      2.43                           1.461
## 48                      2.43                           1.101
## 49                      2.43                           0.845
## 50                      2.43                           1.178
## 51                      2.43                           1.285
## 52                      2.43                           1.021
## 53                      2.43                           1.301
## 54                      2.43                           1.107
## 55                      2.43                           0.693
## 56                      2.43                           1.389
## 57                      2.43                           1.162
## 58                      2.43                           1.323
## 59                      2.43                           0.703
## 60                      2.43                           1.251
## 61                      2.43                           0.853
## 62                      2.43                           1.403
## 63                      2.43                           0.986
## 64                      2.43                           1.032
## 65                      2.43                           0.985
## 66                      2.43                           0.935
## 67                      2.43                           0.665
## 68                      2.43                           1.273
## 69                      2.43                           0.842
## 70                      2.43                           0.966
## 71                      2.43                           0.983
## 72                      2.43                           1.155
## 73                      2.43                           1.106
## 74                      2.43                           1.377
## 75                      2.43                           1.124
## 76                      2.43                           1.241
## 77                      2.43                           1.525
## 78                      2.43                           0.508
## 79                      2.43                           0.817
## 80                      2.43                           1.044
## 81                      2.43                           1.259
## 82                      2.43                           0.954
## 83                      2.43                           0.518
## 84                      2.43                           1.061
## 85                      2.43                           0.669
## 86                      2.43                           0.996
## 87                      2.43                           0.519
## 88                      2.43                           1.181
## 89                      2.43                           1.115
## 90                      2.43                           1.025
## 91                      2.43                           0.543
## 92                      2.43                           0.518
## 93                      2.43                           1.008
## 94                      2.43                           1.068
## 95                      2.43                           0.680
## 96                      2.43                           0.162
## 97                      2.43                           1.046
## 98                      2.43                           0.367
## 99                      2.43                           0.507
## 100                     2.43                           0.808
## 101                     2.43                           0.635
## 102                     2.43                           0.420
## 103                     2.43                           0.967
## 104                     2.43                           1.260
## 105                     2.43                           0.637
## 106                     2.43                           0.792
## 107                     2.43                           0.852
## 108                     2.43                           1.030
## 109                     2.43                           0.946
## 110                     2.43                           0.979
## 111                     2.43                           0.910
## 112                     2.43                           1.037
## 113                     2.43                           0.364
## 114                     2.43                           0.603
## 115                     2.43                           0.183
## 116                     2.43                           0.663
## 117                     2.43                           0.387
## 118                     2.43                           1.030
## 119                     2.43                           0.364
## 120                     2.43                           0.228
## 121                     2.43                           0.603
## 122                     2.43                           0.919
## 123                     2.43                           1.045
## 124                     2.43                           0.882
## 125                     2.43                           0.646
## 126                     2.43                           0.666
## 127                     2.43                           0.890
## 128                     2.43                           0.255
## 129                     2.43                           0.990
## 130                     2.43                           0.849
## 131                     2.43                           0.488
## 132                     2.43                           0.954
## 133                     2.43                           0.370
## 134                     2.43                           0.666
## 135                     2.43                           0.266
## 136                     2.43                           0.254
## 137                     2.43                           0.528
## 138                     2.43                           0.279
## 139                     2.43                           0.741
## 140                     2.43                           0.000
## 141                     2.43                           0.329
## 142                     2.43                           0.433
## 143                     2.43                           0.294
## 144                     2.43                           0.113
## 145                     2.43                           0.451
## 146                     2.43                           1.099
## 147                     2.43                           0.364
## 148                     2.43                           0.457
## 149                     2.43                           0.370
##     explained_by_social_support explained_by_healthy_life_expectancy
## 1                         1.106                                0.741
## 2                         1.108                                0.763
## 3                         1.079                                0.816
## 4                         1.172                                0.772
## 5                         1.079                                0.753
## 6                         1.108                                0.782
## 7                         1.062                                0.763
## 8                         1.003                                0.760
## 9                         1.094                                0.785
## 10                        1.062                                0.782
## 11                        1.076                                0.801
## 12                        1.074                                0.788
## 13                        0.993                                0.757
## 14                        1.044                                0.798
## 15                        1.092                                0.753
## 16                        0.966                                0.722
## 17                        1.062                                0.757
## 18                        1.090                                0.703
## 19                        1.030                                0.621
## 20                        0.998                                0.747
## 21                        1.081                                0.804
## 22                        0.899                                0.662
## 23                        1.055                                0.747
## 24                        0.982                                0.665
## 25                        0.860                                0.594
## 26                        0.964                                0.571
## 27                        1.057                                0.826
## 28                        0.940                                0.798
## 29                        1.093                                0.722
## 30                        0.790                                0.519
## 31                        1.042                                0.649
## 32                        1.019                                0.897
## 33                        0.807                                0.483
## 34                        1.066                                0.653
## 35                        0.944                                0.571
## 36                        0.830                                0.634
## 37                        0.932                                0.599
## 38                        1.065                                0.612
## 39                        0.765                                0.801
## 40                        1.079                                0.640
## 41                        0.976                                0.667
## 42                        1.027                                0.528
## 43                        0.946                                0.678
## 44                        0.982                                0.668
## 45                        1.103                                0.527
## 46                        0.832                                0.595
## 47                        0.857                                0.580
## 48                        0.924                                0.634
## 49                        0.675                                0.565
## 50                        0.996                                0.574
## 51                        1.047                                0.587
## 52                        0.866                                0.615
## 53                        1.083                                0.615
## 54                        0.957                                0.596
## 55                        0.904                                0.604
## 56                        0.949                                0.838
## 57                        0.980                                0.646
## 58                        0.939                                0.760
## 59                        0.787                                0.593
## 60                        1.039                                0.703
## 61                        0.828                                0.426
## 62                        0.758                                0.801
## 63                        0.833                                0.623
## 64                        0.919                                0.618
## 65                        0.888                                0.542
## 66                        0.806                                0.640
## 67                        0.971                                0.501
## 68                        0.811                                0.760
## 69                        0.782                                0.486
## 70                        1.065                                0.442
## 71                        0.970                                0.549
## 72                        0.891                                0.637
## 73                        0.879                                0.555
## 74                        0.806                                0.801
## 75                        1.007                                0.560
## 76                        0.992                                0.511
## 77                        0.841                                0.893
## 78                        0.895                                0.498
## 79                        0.873                                0.616
## 80                        0.821                                0.435
## 81                        0.797                                0.587
## 82                        0.786                                0.433
## 83                        0.392                                0.307
## 84                        0.785                                0.665
## 85                        0.409                                0.052
## 86                        0.758                                0.585
## 87                        0.702                                0.496
## 88                        1.055                                0.583
## 89                        1.015                                0.697
## 90                        0.841                                0.541
## 91                        0.556                                0.159
## 92                        0.558                                0.357
## 93                        0.529                                0.646
## 94                        0.772                                0.535
## 95                        0.595                                0.287
## 96                        0.402                                0.167
## 97                        1.172                                0.439
## 98                        0.511                                0.210
## 99                        0.058                                0.196
## 100                       0.598                                0.330
## 101                       0.520                                0.514
## 102                       0.399                                0.206
## 103                       0.895                                0.265
## 104                       0.809                                0.590
## 105                       0.423                                0.322
## 106                       0.219                                0.558
## 107                       0.897                                0.574
## 108                       0.470                                0.498
## 109                       0.765                                0.552
## 110                       0.958                                0.517
## 111                       0.638                                0.381
## 112                       0.707                                0.362
## 113                       0.472                                0.179
## 114                       0.680                                0.426
## 115                       0.634                                0.196
## 116                       0.625                                0.051
## 117                       0.590                                0.110
## 118                       0.557                                0.561
## 119                       0.718                                0.240
## 120                       0.580                                0.253
## 121                       0.508                                0.385
## 122                       0.515                                0.590
## 123                       0.868                                0.595
## 124                       0.801                                0.262
## 125                       0.819                                0.434
## 126                       0.713                                0.341
## 127                       0.685                                0.583
## 128                       0.353                                0.000
## 129                       0.820                                0.593
## 130                       0.693                                0.074
## 131                       0.367                                0.279
## 132                       0.647                                0.426
## 133                       0.679                                0.331
## 134                       0.749                                0.273
## 135                       0.503                                0.341
## 136                       0.239                                0.203
## 137                       0.552                                0.231
## 138                       0.377                                0.100
## 139                       0.316                                0.383
## 140                       0.062                                0.155
## 141                       0.831                                0.272
## 142                       0.540                                0.300
## 143                       0.173                                0.227
## 144                       0.168                                0.298
## 145                       0.731                                0.007
## 146                       0.724                                0.340
## 147                       0.202                                0.407
## 148                       0.649                                0.243
## 149                       0.000                                0.126
##     explained_by_freedom_to_make_life_choices explained_by_generosity
## 1                                       0.691                   0.124
## 2                                       0.686                   0.208
## 3                                       0.653                   0.204
## 4                                       0.698                   0.293
## 5                                       0.647                   0.302
## 6                                       0.703                   0.249
## 7                                       0.685                   0.244
## 8                                       0.639                   0.166
## 9                                       0.665                   0.276
## 10                                      0.640                   0.215
## 11                                      0.647                   0.291
## 12                                      0.509                   0.208
## 13                                      0.600                   0.195
## 14                                      0.648                   0.246
## 15                                      0.606                   0.238
## 16                                      0.673                   0.105
## 17                                      0.580                   0.340
## 18                                      0.580                   0.052
## 19                                      0.554                   0.252
## 20                                      0.489                   0.088
## 21                                      0.536                   0.092
## 22                                      0.661                   0.246
## 23                                      0.664                   0.275
## 24                                      0.490                   0.142
## 25                                      0.670                   0.236
## 26                                      0.603                   0.090
## 27                                      0.462                   0.135
## 28                                      0.379                   0.133
## 29                                      0.690                   0.122
## 30                                      0.638                   0.163
## 31                                      0.625                   0.128
## 32                                      0.664                   0.176
## 33                                      0.593                   0.356
## 34                                      0.468                   0.107
## 35                                      0.514                   0.142
## 36                                      0.585                   0.092
## 37                                      0.618                   0.099
## 38                                      0.476                   0.056
## 39                                      0.464                   0.178
## 40                                      0.641                   0.119
## 41                                      0.596                   0.079
## 42                                      0.716                   0.391
## 43                                      0.438                   0.159
## 44                                      0.558                   0.080
## 45                                      0.573                   0.143
## 46                                      0.564                   0.045
## 47                                      0.591                   0.120
## 48                                      0.482                   0.189
## 49                                      0.615                   0.116
## 50                                      0.590                   0.153
## 51                                      0.405                   0.082
## 52                                      0.554                   0.100
## 53                                      0.454                   0.067
## 54                                      0.611                   0.375
## 55                                      0.553                   0.201
## 56                                      0.504                   0.020
## 57                                      0.544                   0.069
## 58                                      0.621                   0.029
## 59                                      0.578                   0.241
## 60                                      0.453                   0.111
## 61                                      0.651                   0.125
## 62                                      0.353                   0.134
## 63                                      0.536                   0.087
## 64                                      0.395                   0.261
## 65                                      0.536                   0.137
## 66                                      0.560                   0.107
## 67                                      0.673                   0.266
## 68                                      0.243                   0.000
## 69                                      0.600                   0.138
## 70                                      0.397                   0.263
## 71                                      0.602                   0.206
## 72                                      0.397                   0.166
## 73                                      0.581                   0.101
## 74                                      0.503                   0.196
## 75                                      0.326                   0.070
## 76                                      0.409                   0.115
## 77                                      0.408                   0.232
## 78                                      0.548                   0.152
## 79                                      0.679                   0.124
## 80                                      0.474                   0.131
## 81                                      0.624                   0.270
## 82                                      0.598                   0.541
## 83                                      0.381                   0.144
## 84                                      0.636                   0.093
## 85                                      0.438                   0.177
## 86                                      0.540                   0.079
## 87                                      0.488                   0.287
## 88                                      0.494                   0.125
## 89                                      0.575                   0.204
## 90                                      0.526                   0.043
## 91                                      0.425                   0.205
## 92                                      0.381                   0.158
## 93                                      0.491                   0.168
## 94                                      0.450                   0.212
## 95                                      0.517                   0.268
## 96                                      0.516                   0.200
## 97                                      0.602                   0.366
## 98                                      0.384                   0.465
## 99                                      0.457                   0.166
## 100                                     0.643                   0.268
## 101                                     0.603                   0.161
## 102                                     0.384                   0.250
## 103                                     0.447                   0.144
## 104                                     0.236                   0.097
## 105                                     0.418                   0.252
## 106                                     0.477                   0.034
## 107                                     0.284                   0.078
## 108                                     0.488                   0.032
## 109                                     0.119                   0.144
## 110                                     0.417                   0.181
## 111                                     0.302                   0.153
## 112                                     0.424                   0.058
## 113                                     0.381                   0.182
## 114                                     0.702                   0.210
## 115                                     0.608                   0.228
## 116                                     0.433                   0.212
## 117                                     0.384                   0.164
## 118                                     0.275                   0.330
## 119                                     0.398                   0.267
## 120                                     0.430                   0.221
## 121                                     0.483                   0.375
## 122                                     0.334                   0.057
## 123                                     0.175                   0.140
## 124                                     0.411                   0.091
## 125                                     0.330                   0.082
## 126                                     0.601                   0.520
## 127                                     0.455                   0.079
## 128                                     0.240                   0.215
## 129                                     0.559                   0.239
## 130                                     0.323                   0.067
## 131                                     0.202                   0.241
## 132                                     0.446                   0.069
## 133                                     0.451                   0.241
## 134                                     0.218                   0.119
## 135                                     0.207                   0.185
## 136                                     0.289                   0.209
## 137                                     0.487                   0.227
## 138                                     0.408                   0.243
## 139                                     0.622                   0.246
## 140                                     0.298                   0.172
## 141                                     0.268                   0.092
## 142                                     0.549                   0.307
## 143                                     0.257                   0.463
## 144                                     0.484                   0.213
## 145                                     0.405                   0.103
## 146                                     0.539                   0.027
## 147                                     0.627                   0.227
## 148                                     0.359                   0.157
## 149                                     0.000                   0.122
##     explained_by_perceptions_of_corruption dystopia_residual
## 1                                    0.481             3.253
## 2                                    0.485             2.868
## 3                                    0.413             2.839
## 4                                    0.170             2.967
## 5                                    0.384             2.798
## 6                                    0.427             2.580
## 7                                    0.448             2.683
## 8                                    0.353             2.653
## 9                                    0.445             2.612
## 10                                   0.292             2.784
## 11                                   0.317             2.598
## 12                                   0.119             3.083
## 13                                   0.306             2.824
## 14                                   0.335             2.585
## 15                                   0.367             2.384
## 16                                   0.083             3.387
## 17                                   0.306             2.596
## 18                                   0.046             3.124
## 19                                   0.154             2.807
## 20                                   0.187             2.862
## 21                                   0.235             2.521
## 22                                   0.139             2.631
## 23                                   0.183             2.268
## 24                                   0.139             2.687
## 25                                   0.223             2.422
## 26                                   0.163             2.668
## 27                                   0.124             2.513
## 28                                   0.047             2.794
## 29                                   0.085             2.388
## 30                                   0.105             3.375
## 31                                   0.223             2.600
## 32                                   0.547             1.379
## 33                                   0.014             3.182
## 34                                   0.018             2.714
## 35                                   0.117             3.015
## 36                                   0.089             2.961
## 37                                   0.035             3.135
## 38                                   0.073             2.624
## 39                                   0.061             2.578
## 40                                   0.263             2.103
## 41                                   0.053             2.509
## 42                                   0.271             2.477
## 43                                   0.070             2.682
## 44                                   0.130             2.438
## 45                                   0.132             2.446
## 46                                   0.001             2.830
## 47                                   0.130             2.368
## 48                                   0.066             2.682
## 49                                   0.160             3.085
## 50                                   0.096             2.462
## 51                                   0.089             2.536
## 52                                   0.063             2.794
## 53                                   0.040             2.432
## 54                                   0.028             2.309
## 55                                   0.176             2.841
## 56                                   0.192             2.048
## 57                                   0.067             2.461
## 58                                   0.033             2.225
## 59                                   0.083             2.934
## 60                                   0.000             2.325
## 61                                   0.126             2.872
## 62                                   0.135             2.262
## 63                                   0.031             2.744
## 64                                   0.005             2.583
## 65                                   0.013             2.665
## 66                                   0.062             2.653
## 67                                   0.020             2.648
## 68                                   0.074             2.561
## 69                                   0.064             2.805
## 70                                   0.053             2.492
## 71                                   0.037             2.306
## 72                                   0.081             2.254
## 73                                   0.144             2.178
## 74                                   0.200             1.653
## 75                                   0.199             2.247
## 76                                   0.060             2.148
## 77                                   0.342             1.236
## 78                                   0.247             2.619
## 79                                   0.091             2.211
## 80                                   0.174             2.331
## 81                                   0.064             1.784
## 82                                   0.046             1.987
## 83                                   0.124             3.476
## 84                                   0.117             1.982
## 85                                   0.092             3.469
## 86                                   0.198             2.127
## 87                                   0.135             2.642
## 88                                   0.005             1.823
## 89                                   0.073             1.520
## 90                                   0.276             1.919
## 91                                   0.058             3.195
## 92                                   0.088             3.071
## 93                                   0.024             2.250
## 94                                   0.022             2.042
## 95                                   0.058             2.684
## 96                                   0.157             3.470
## 97                                   0.033             1.409
## 98                                   0.123             2.990
## 99                                   0.178             3.482
## 100                                  0.179             2.204
## 101                                  0.164             2.427
## 102                                  0.111             3.216
## 103                                  0.051             2.187
## 104                                  0.104             1.852
## 105                                  0.097             2.784
## 106                                  0.088             2.749
## 107                                  0.072             2.135
## 108                                  0.181             2.191
## 109                                  0.120             2.242
## 110                                  0.010             1.813
## 111                                  0.041             2.429
## 112                                  0.064             2.201
## 113                                  0.122             3.133
## 114                                  0.061             2.148
## 115                                  0.163             2.783
## 116                                  0.039             2.736
## 117                                  0.072             3.016
## 118                                  0.144             1.823
## 119                                  0.054             2.596
## 120                                  0.057             2.857
## 121                                  0.073             2.180
## 122                                  0.044             2.138
## 123                                  0.026             1.736
## 124                                  0.059             2.068
## 125                                  0.075             2.131
## 126                                  0.178             1.407
## 127                                  0.150             1.553
## 128                                  0.084             3.209
## 129                                  0.049             1.075
## 130                                  0.147             2.155
## 131                                  0.101             2.610
## 132                                  0.092             1.648
## 133                                  0.114             2.089
## 134                                  0.133             2.069
## 135                                  0.087             2.620
## 136                                  0.107             2.806
## 137                                  0.074             1.975
## 138                                  0.047             2.396
## 139                                  0.106             1.405
## 140                                  0.212             2.876
## 141                                  0.089             1.776
## 142                                  0.231             1.263
## 143                                  0.139             2.060
## 144                                  0.134             2.190
## 145                                  0.015             1.800
## 146                                  0.088             0.648
## 147                                  0.493             1.095
## 148                                  0.075             1.205
## 149                                  0.010             1.895
```

#Structural Analysis


```r
names(happy)
```

```
##  [1] "country_name"                             
##  [2] "regional_indicator"                       
##  [3] "ladder_score"                             
##  [4] "standard_error_of_ladder_score"           
##  [5] "upperwhisker"                             
##  [6] "lowerwhisker"                             
##  [7] "logged_gdp_per_capita"                    
##  [8] "social_support"                           
##  [9] "healthy_life_expectancy"                  
## [10] "freedom_to_make_life_choices"             
## [11] "generosity"                               
## [12] "perceptions_of_corruption"                
## [13] "ladder_score_in_dystopia"                 
## [14] "explained_by_log_gdp_per_capita"          
## [15] "explained_by_social_support"              
## [16] "explained_by_healthy_life_expectancy"     
## [17] "explained_by_freedom_to_make_life_choices"
## [18] "explained_by_generosity"                  
## [19] "explained_by_perceptions_of_corruption"   
## [20] "dystopia_residual"
```


```r
glimpse(happy)
```

```
## Rows: 149
## Columns: 20
## $ country_name                              <chr> "Finland", "Denmark", "Switz…
## $ regional_indicator                        <chr> "Western Europe", "Western E…
## $ ladder_score                              <dbl> 7.842, 7.620, 7.571, 7.554, …
## $ standard_error_of_ladder_score            <dbl> 0.032, 0.035, 0.036, 0.059, …
## $ upperwhisker                              <dbl> 7.904, 7.687, 7.643, 7.670, …
## $ lowerwhisker                              <dbl> 7.780, 7.552, 7.500, 7.438, …
## $ logged_gdp_per_capita                     <dbl> 10.775, 10.933, 11.117, 10.8…
## $ social_support                            <dbl> 0.954, 0.954, 0.942, 0.983, …
## $ healthy_life_expectancy                   <dbl> 72.000, 72.700, 74.400, 73.0…
## $ freedom_to_make_life_choices              <dbl> 0.949, 0.946, 0.919, 0.955, …
## $ generosity                                <dbl> -0.098, 0.030, 0.025, 0.160,…
## $ perceptions_of_corruption                 <dbl> 0.186, 0.179, 0.292, 0.673, …
## $ ladder_score_in_dystopia                  <dbl> 2.43, 2.43, 2.43, 2.43, 2.43…
## $ explained_by_log_gdp_per_capita           <dbl> 1.446, 1.502, 1.566, 1.482, …
## $ explained_by_social_support               <dbl> 1.106, 1.108, 1.079, 1.172, …
## $ explained_by_healthy_life_expectancy      <dbl> 0.741, 0.763, 0.816, 0.772, …
## $ explained_by_freedom_to_make_life_choices <dbl> 0.691, 0.686, 0.653, 0.698, …
## $ explained_by_generosity                   <dbl> 0.124, 0.208, 0.204, 0.293, …
## $ explained_by_perceptions_of_corruption    <dbl> 0.481, 0.485, 0.413, 0.170, …
## $ dystopia_residual                         <dbl> 3.253, 2.868, 2.839, 2.967, …
```

#NA Summary

```r
naniar::miss_var_summary(happy)
```

```
## # A tibble: 20 × 3
##    variable                                  n_miss pct_miss
##    <chr>                                      <int>    <dbl>
##  1 country_name                                   0        0
##  2 regional_indicator                             0        0
##  3 ladder_score                                   0        0
##  4 standard_error_of_ladder_score                 0        0
##  5 upperwhisker                                   0        0
##  6 lowerwhisker                                   0        0
##  7 logged_gdp_per_capita                          0        0
##  8 social_support                                 0        0
##  9 healthy_life_expectancy                        0        0
## 10 freedom_to_make_life_choices                   0        0
## 11 generosity                                     0        0
## 12 perceptions_of_corruption                      0        0
## 13 ladder_score_in_dystopia                       0        0
## 14 explained_by_log_gdp_per_capita                0        0
## 15 explained_by_social_support                    0        0
## 16 explained_by_healthy_life_expectancy           0        0
## 17 explained_by_freedom_to_make_life_choices      0        0
## 18 explained_by_generosity                        0        0
## 19 explained_by_perceptions_of_corruption         0        0
## 20 dystopia_residual                              0        0
```
