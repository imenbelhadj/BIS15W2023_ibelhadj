---
title: "Lab 4 Homework"
author: "Imen Belhadj"
date: "2023-01-23"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library("tidyverse")
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
dim(homerange)
```

```
## [1] 569  24
```

```r
colnames(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
homerange_variables <-colnames(homerange)
class(homerange_variables)
```

```
## [1] "character"
```

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
homerange$taxon <- as.factor(homerange$taxon)
homerange$order <- as.factor(homerange$order)
```

```r
select_if(homerange, is.factor)
```

```
## # A tibble: 569 × 2
##    taxon         order         
##    <fct>         <fct>         
##  1 lake fishes   anguilliformes
##  2 river fishes  cypriniformes 
##  3 river fishes  cypriniformes 
##  4 river fishes  cypriniformes 
##  5 river fishes  cypriniformes 
##  6 river fishes  esociformes   
##  7 marine fishes gadiformes    
##  8 marine fishes gadiformes    
##  9 marine fishes perciformes   
## 10 marine fishes perciformes   
## # … with 559 more rows
```

```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tinamiformes"          "tetraodontiformes\xa0"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
taxa <- select(homerange, "taxon", "class", "order", "family", "genus", "species")
taxa
```

```
## # A tibble: 569 × 6
##    taxon         class          order          family       genus       species 
##    <fct>         <chr>          <fct>          <chr>        <chr>       <chr>   
##  1 lake fishes   actinopterygii anguilliformes anguillidae  anguilla    rostrata
##  2 river fishes  actinopterygii cypriniformes  catostomidae moxostoma   poecilu…
##  3 river fishes  actinopterygii cypriniformes  cyprinidae   campostoma  anomalum
##  4 river fishes  actinopterygii cypriniformes  cyprinidae   clinostomus fundulo…
##  5 river fishes  actinopterygii cypriniformes  cyprinidae   rhinichthys catarac…
##  6 river fishes  actinopterygii esociformes    esocidae     esox        masquin…
##  7 marine fishes actinopterygii gadiformes     gadidae      pollachius  pollach…
##  8 marine fishes actinopterygii gadiformes     gadidae      pollachius  virens  
##  9 marine fishes actinopterygii perciformes    acanthuridae acanthurus  lineatus
## 10 marine fishes actinopterygii perciformes    acanthuridae naso        liturat…
## # … with 559 more rows
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
taxa %>% group_by(species, taxon) %>% tally()
```

```
## # A tibble: 544 × 3
## # Groups:   species [517]
##    species          taxon             n
##    <chr>            <fct>         <int>
##  1 aberti           birds             1
##  2 aberti           mammals           1
##  3 adspersus        marine fishes     1
##  4 aedon            birds             1
##  5 aegyptius        lizards           1
##  6 aethiopicus      mammals           1
##  7 africaeaustralis mammals           1
##  8 africana         mammals           1
##  9 africanus        mammals           1
## 10 agassizii        tortoises         1
## # … with 534 more rows
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
table(homerange$species, homerange$trophic.guild)
```

```
##                           
##                            carnivore herbivore
##   aberti                           0         2
##   adspersus                        1         0
##   aedon                            1         0
##   aegyptius                        0         1
##   aethiopicus                      0         1
##   africaeaustralis                 0         1
##   africana                         0         1
##   africanus                        0         1
##   agassizii                        0         1
##   agrestis                         0         1
##   alba                             2         0
##   albicauda                        1         0
##   alces                            0         1
##   aluco                            1         0
##   americana                        2         2
##   americanus                       1         2
##   ammon                            0         1
##   amoenus                          0         1
##   analis                           1         0
##   annularis                        1         0
##   anomalum                         1         0
##   antilopinus                      0         1
##   antimena                         0         1
##   apicalis                         0         1
##   apodus                           1         0
##   aquaticus                        1         2
##   arborea                          2         0
##   arcticus                         1         1
##   areolatus                        1         0
##   argenteocinereus                 0         1
##   argi                             0         1
##   argus                            1         0
##   aruanus                          1         0
##   asper                            1         0
##   assimilis                        0         1
##   atlanticus                       0         1
##   atricapillus                     2         0
##   atrox                            1         0
##   audeberti                        0         1
##   auratus                          2         0
##   auritus                          1         0
##   aurocapillus                     1         0
##   aurofrenatum                     0         1
##   australis                        1         0
##   avellanarius                     0         1
##   axis                             0         1
##   bairdi                           1         0
##   barbata                          1         0
##   baronessa                        1         0
##   beecheyi                         0         1
##   belli                            1         0
##   bengalensis                      1         0
##   bergylta                         1         0
##   bewickiI                         1         0
##   bezoarticus                      0         1
##   biarmicus                        1         0
##   bicolor                          0         1
##   bicornis                         0         1
##   bifasciatum                      1         0
##   biocellata                       0         1
##   bison                            0         1
##   bivittatus                       1         0
##   blandingii                       1         0
##   bonaci                           1         0
##   bonasia                          0         1
##   bonasus                          0         1
##   bonelli                          1         0
##   bottae                           0         1
##   bubo                             1         0
##   bungaroides                      1         0
##   buselaphus                       0         1
##   buteo                            1         0
##   butleri                          1         0
##   caballus                         0         1
##   cabrilla                         1         0
##   californianus                    1         0
##   californicus                     0         3
##   callipygus                       0         1
##   camelopardalis                   0         1
##   camelus                          0         1
##   campestris                       0         1
##   canadensis                       2         1
##   cannabina                        0         1
##   canorus                          1         0
##   canus                            1         0
##   capensis                         0         2
##   capreolus                        0         1
##   caracal                          1         0
##   carbonaria                       0         1
##   carolinae                        1         0
##   carolinensis                     1         1
##   caryocatactes                    0         1
##   cataractae                       1         0
##   catenifer                        1         0
##   catus                            1         0
##   caudatus                         1         0
##   caurinus                         1         0
##   cerastes                         1         0
##   cheriway                         1         0
##   chromis                          0         1
##   chrysaetos                       1         0
##   chrysopterum                     0         1
##   chrysopygus                      1         0
##   chrysurus                        1         0
##   cinerea                          0         1
##   cinereus                         1         0
##   citrea                           1         0
##   clarki                           1         0
##   clathratus                       1         0
##   coelebs                          1         0
##   collurio                         1         0
##   columbianus                      0         1
##   concolor                         1         0
##   constrictor                      1         0
##   constrictor flaviventris         1         0
##   contortrix                       1         0
##   cooperi                          0         1
##   cooperii                         1         0
##   corax                            1         0
##   coronatus                        1         0
##   couperi                          1         0
##   crex                             0         1
##   cristata                         1         0
##   cristatus                        1         0
##   cruentata                        1         0
##   culpaeus                         1         0
##   cuniculus                        0         1
##   cupido pinnatus                  0         1
##   curzoniae                        0         1
##   cuvieri                          0         1
##   cyanea                           1         0
##   cyaneus                          1         0
##   cyanus                           0         1
##   cyclura                          0         1
##   dahli                            1         0
##   dalli                            1         0
##   dama                             0         1
##   damarensis                       0         1
##   decussatus                       1         0
##   dentirostris                     0         1
##   dimidiatus                       1         0
##   dolomieu                         1         0
##   dorsalis                         0         3
##   dorsatum                         0         1
##   elaphus                          0         1
##   elegans                          2         0
##   epops                            1         0
##   erminea                          1         0
##   erythrogaster                    1         0
##   erythropus                       0         1
##   europaea                         2         0
##   europaeus                        2         1
##   exilis                           1         0
##   falco                            1         0
##   familiaris                       1         0
##   fasciata                         1         0
##   fasciatus                        1         0
##   ferox                            1         0
##   flagellifer                      0         1
##   flagellum                        1         0
##   flava                            1         0
##   flavescens                       1         0
##   flavicollis                      0         1
##   flavimaculata                    1         0
##   flaviventris                     0         1
##   flavolineatus                    1         0
##   flavus                           0         1
##   floridanus                       0         1
##   foina                            1         0
##   fraenata                         0         1
##   franklinii                       0         1
##   frenata                          1         0
##   fulgens                          0         1
##   fuliginosus                      0         1
##   funduloides                      1         0
##   funereus                         1         0
##   furo                             1         0
##   fusca                            1         0
##   fuscicauda                       1         0
##   fuscipes                         0         1
##   fuscus                           0         2
##   gaimardi                         0         1
##   gallicus                         1         0
##   galloti                          0         1
##   garnoti                          1         0
##   garrulus                         1         0
##   gazella                          0         1
##   genetta                          1         0
##   gentilis                         1         0
##   geoffroii                        1         0
##   geoffroyi                        1         0
##   getula getula                    1         0
##   gibbosus                         1         0
##   gigal                            1         0
##   giganteus                        0         1
##   gilae                            1         0
##   glaber                           0         1
##   glandarius                       1         0
##   gobio                            1         0
##   gossypinus                       1         0
##   gracillimus                      1         0
##   graeca                           0         1
##   granti                           1         0
##   griseus                          3         0
##   guentheri                        0         1
##   gulo                             1         0
##   guttata emoryi                   1         0
##   guttatus                         1         0
##   guttulatus                       1         0
##   habroptilus                      0         1
##   harak                            1         0
##   hemionus                         0         1
##   hemistiktos                      1         0
##   hermanii                         0         1
##   hipoliti                         1         0
##   hircus                           0         1
##   hispidua                         0         1
##   horridus                         1         0
##   horsfieldi                       0         1
##   hottentotus                      0         1
##   hudsonicus                       0         1
##   huntii                           1         0
##   hurrianae                        0         1
##   idahoensis                       0         1
##   ignicapillus                     1         0
##   ignobilis                        1         0
##   impressa                         0         1
##   inca                             0         1
##   inchneumon                       1         0
##   indica                           0         1
##   inermis                          1         0
##   ingens                           0         1
##   inornatus                        1         0
##   iseri                            0         1
##   jamaicensis                      1         0
##   japonica                         1         0
##   johnstoni                        0         1
##   jubatus                          1         0
##   julis                            1         0
##   juncidis                         1         0
##   kirtlandi                        1         0
##   kleinmanni                       0         1
##   krefftii                         0         1
##   labrax                           1         0
##   lagopus                          1         1
##   latastei                         1         0
##   leopardus                        1         0
##   lepida                           0         1
##   leprosa                          0         1
##   lervia                           0         1
##   leucopus                         1         0
##   leucotos                         1         0
##   lewisi                           0         1
##   lineatus                         1         1
##   lineolatus                       1         0
##   lis                              0         1
##   lituratus                        0         1
##   longicollis                      1         0
##   longipes                         0         1
##   longipinnis                      1         0
##   longissimus                      1         0
##   ludovicianus                     2         0
##   lumbriciformis                   1         0
##   lumholtzi                        0         1
##   lunare                           1         0
##   luridus                          1         0
##   lutreola                         1         0
##   lynx                             1         0
##   maccullochi                      1         0
##   macrochirus                      1         0
##   macroti                          1         0
##   maculatus                        1         0
##   maculipinna                      1         0
##   magna                            1         0
##   magnolia                         1         0
##   major                            0         1
##   maliger                          1         0
##   marginatus                       1         0
##   marmoratus                       1         0
##   martes                           1         0
##   martius                          1         0
##   masquinongy                      1         0
##   maximus                          0         2
##   medius                           1         0
##   megacephalus                     0         1
##   megalotis                        1         0
##   melampus                         0         1
##   melanoleuca                      0         1
##   melanoleucus                     1         0
##   melanops                         1         0
##   merriami                         0         1
##   mexicanus                        1         0
##   micropus                         0         1
##   microrhinos                      0         1
##   milvus                           1         0
##   miniata                          1         0
##   minimus                          1         1
##   minor                            1         0
##   minor peltifer                   1         0
##   molossus                         1         0
##   monax                            0         1
##   montanus                         0         1
##   morio                            1         0
##   mustinus                         1         0
##   mykiss                           1         0
##   natalis                          1         0
##   natrix                           1         0
##   nebulifer                        1         0
##   neglecta                         1         0
##   nicholsii                        1         0
##   niger                            0         1
##   nigricollis                      0         1
##   nigripes                         1         0
##   nippon                           0         1
##   nisus                            1         0
##   nivalis                          1         0
##   noctua                           1         0
##   obesulus                         1         0
##   obesus                           0         1
##   obscurus                         0         1
##   obsoleta                         1         0
##   ochrogaster                      0         1
##   ocularis                         0         1
##   odoratus                         1         0
##   oenanthe                         1         0
##   olivaceus                        1         0
##   onca                             1         0
##   orbicularis                      1         0
##   ordii                            0         1
##   oreganus concolor                1         0
##   ornata                           0         2
##   oryx                             0         1
##   ostralegus                       1         0
##   otus                             1         0
##   palliatus                        0         1
##   pallidus                         0         1
##   paludinosus                      1         0
##   palumbus                         0         1
##   palustris                        1         1
##   pardalis                         1         1
##   pardinus                         1         0
##   pardus                           1         0
##   parryii                          0         1
##   partitus                         0         1
##   parvula                          1         0
##   passerina                        1         0
##   passerinum                       1         0
##   patagonus                        0         1
##   pecari                           0         1
##   penicillata                      1         0
##   pennanti                         1         1
##   pennata                          0         1
##   pennatus                         1         0
##   pennsylvanicus                   0         1
##   pensylvanica                     1         0
##   percnopterus                     1         0
##   perdix                           0         1
##   peregrinus                       1         0
##   petechia                         1         0
##   philadelphia                     1         0
##   phoenicurus                      1         0
##   picta marginata                  1         0
##   pinetorum                        0         1
##   pinguis                          0         1
##   pinos                            1         0
##   piscivorous                      1         0
##   platirhinos                      1         0
##   poecilura                        1         0
##   poeyi                            1         0
##   pollachius                       1         0
##   polyglotta                       1         0
##   polyglottos                      1         0
##   polyphemus                       0         1
##   porphyreus                       1         0
##   porphyriacus                     1         0
##   prehensilis                      0         1
##   pricei                           1         0
##   princeps                         1         1
##   puda                             0         1
##   pulcher                          1         0
##   pumilio                          0         1
##   punctatus                        1         0
##   pygargus                         1         0
##   pyrenaica                        0         1
##   quadrivittatus                   0         1
##   raddei                           1         0
##   radiolosus                       1         0
##   raimondii                        0         1
##   raviventris                      0         1
##   reevesi                          0         1
##   regulus                          1         0
##   reticularia                      1         0
##   richardsoni                      0         1
##   rivulatus                        0         1
##   robustus                         0         1
##   romana                           1         0
##   rostrata                         2         0
##   rubetra                          1         0
##   rubica                           1         0
##   rubripinne                       0         1
##   rubrubrum                        1         0
##   rufa                             0         1
##   rufescens                        1         0
##   rufodorsatus                     1         0
##   rufogriseus                      0         1
##   rufus                            2         2
##   rupestris                        1         0
##   rupicapra                        0         1
##   ruppelli                         1         0
##   russula                          1         0
##   ruticilla                        1         0
##   sabrinus                         0         1
##   salar                            1         0
##   salmoides                        1         0
##   salpa                            0         1
##   sarda                            1         0
##   savannarum                       1         0
##   scandiaca                        1         0
##   schisticolor                     0         1
##   schneideri                       1         0
##   scriba                           1         0
##   scriptus                         0         1
##   scutatus                         1         0
##   scutulatus                       1         0
##   sectatrix                        0         1
##   semispinosus                     0         1
##   senator                          1         0
##   serinus                          1         0
##   serpentina                       1         0
##   serval                           1         0
##   shedaoensis                      1         0
##   sialis                           1         0
##   sibirica                         1         0
##   sibiricus                        0         2
##   simensis                         1         0
##   simum                            0         1
##   sipeodon                         1         0
##   sparverius                       1         0
##   spectabilis                      0         1
##   spectrabilis                     1         0
##   spekii                           0         1
##   spilosoma                        0         1
##   spilota imbricata                1         0
##   spinifera                        1         0
##   splendens                        1         0
##   stellaris                        1         0
##   stephensi                        0         1
##   stigmatica                       0         1
##   strepera                         0         1
##   strepsiceros                     0         1
##   striata                          1         0
##   striatus                         2         0
##   stuartii                         1         0
##   suillus                          0         1
##   swainsoni                        1         0
##   sylvaticus                       0         1
##   sylvestris                       1         0
##   tajacu                           0         1
##   tarandus                         0         1
##   tauvina                          1         0
##   taxus                            1         0
##   telum                            0         1
##   tentorius                        0         1
##   tetradactylus                    1         0
##   tetrix                           0         1
##   thetis                           0         1
##   tigrina                          1         0
##   tigris                           2         0
##   timidus                          0         1
##   tinnunculus                      1         0
##   torquatus                        0         1
##   torquilla                        1         0
##   torridus                         1         0
##   travancorica                     0         1
##   trevelyani                       1         0
##   triangulum                       1         0
##   trichas                          1         0
##   trichrous                        1         0
##   tridactylus                      1         0
##   tridecemlineatus                 0         1
##   trifascialis                     1         0
##   trifasciatus                     1         0
##   troglodytes                      1         0
##   trutta                           1         0
##   turtur                           0         1
##   tyrannus                         1         0
##   umbrinus                         0         1
##   uncia                            1         0
##   undata                           1         0
##   undulatus                        1         0
##   unguiculatus                     1         0
##   unicornis                        0         1
##   unimaculatus                     1         0
##   urogallus                        0         1
##   urophasianus                     0         1
##   ursinus                          1         1
##   variabilis                       0         1
##   variegatus                       0         1
##   velox                            1         0
##   vermis                           1         0
##   virens                           4         0
##   virginianus                      1         1
##   viride                           0         1
##   viridiflavus                     1         0
##   viridis                          2         0
##   vittata                          1         0
##   volans                           0         2
##   vulgaris                         0         1
##   vulpecula                        0         1
##   wagneri                          0         1
##   wardi                            0         1
##   wiedii                           1         0
##   wolfi                            1         0
##   wrightii                         1         0
##   yagouaroundi                     1         0
##   zibetha                          1         0
##   zibethica                        0         1
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivores <- filter(homerange, trophic.guild=="carnivore")
```

```r
herbivores <-filter(homerange, trophic.guild=="herbivore")
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
is.na(carnivores$mean.hra.m2)
```

```
##   [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [13] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [25] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [37] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [61] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [73] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [85] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [97] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [109] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [121] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [133] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [145] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [157] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [169] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [181] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [193] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [205] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [217] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [229] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [241] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [253] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [265] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [277] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [289] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [301] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [313] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [325] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [337] FALSE FALSE FALSE FALSE FALSE FALSE
```

```r
is.na(herbivores$mean.hra.m2)
```

```
##   [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [13] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [25] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [37] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [61] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [73] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [85] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [97] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [109] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [121] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [133] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [145] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [157] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [169] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [181] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [193] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [205] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
## [217] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
```

```r
#There are no NAs in the mean.hra.m2 columns for herbivores and carnivores.
```

```r
mean(herbivores$mean.hra.m2)
```

```
## [1] 34137012
```

```r
mean(carnivores$mean.hra.m2)
```

```
## [1] 13039918
```

```r
#Herbivores have a higher mean.hra.m2 than carnivores. 
```

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  

```r
deer<- select(homerange, "log10.mass", "family", "genus", "mean.mass.g")
```

```r
deer1 <- filter(deer, family== "cervidae")
deer1
```

```
## # A tibble: 12 × 4
##    log10.mass family   genus      mean.mass.g
##         <dbl> <chr>    <chr>            <dbl>
##  1       5.49 cervidae alces          307227.
##  2       4.80 cervidae axis            62823.
##  3       4.38 cervidae capreolus       24050.
##  4       5.37 cervidae cervus         234758.
##  5       4.47 cervidae cervus          29450.
##  6       4.85 cervidae dama            71450.
##  7       4.13 cervidae muntiacus       13500.
##  8       4.73 cervidae odocoileus      53864.
##  9       4.94 cervidae odocoileus      87884.
## 10       4.54 cervidae ozotoceros      35000.
## 11       3.88 cervidae pudu             7500.
## 12       5.01 cervidae rangifer       102059.
```

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    

```r
snakes<-select(homerange, "species", "taxon","mean.hra.m2")
```

```r
snakes1 <- filter(snakes, taxon=="snakes")
snakes1
```

```
## # A tibble: 41 × 3
##    species                  taxon  mean.hra.m2
##    <chr>                    <fct>        <dbl>
##  1 vermis                   snakes         700
##  2 viridis                  snakes         253
##  3 constrictor              snakes      151000
##  4 constrictor flaviventris snakes      114500
##  5 punctatus                snakes        6476
##  6 couperi                  snakes     1853000
##  7 guttata emoryi           snakes      150600
##  8 obsoleta                 snakes       46000
##  9 platirhinos              snakes      516375
## 10 viridiflavus             snakes      110900
## # … with 31 more rows
```

```r
min(snakes1[,3])
```

```
## [1] 200
```

```r
#The snake with the smallest home range is the schneideri snake.Also known as "Bitis schneideri", it is a venemous snake that lives natively in Southern Africa.It is possibly the smallest viper in the world.
```
## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
