# Some JDK tests...

## corretto-8.222.10.1

```
"Elapsed time: 10956.74844 msecs"
"Elapsed time: 4486.034422 msecs"
```

## 8.0.222.j9-adpt

```
"Elapsed time: 6654.354136 msecs"
"Elapsed time: 3714.212684 msecs"
```

## 8.0.222.hs-adpt

```
"Elapsed time: 10512.722145 msecs"
"Elapsed time: 4029.348681 msecs"
```

## 11.0.4-amzn

```
"Elapsed time: 12287.995344 msecs"
"Elapsed time: 4493.021668 msecs"
```

## 11.0.4.j9-adpt

```
"Elapsed time: 7067.861256 msecs"
"Elapsed time: 4371.907519 msecs"
```

## 12.0.2.hs-adpt

```
"Elapsed time: 14311.87187 msecs"
"Elapsed time: 13775.201107 msecs"
```

## 12.0.2.j9-adpt

```
"Elapsed time: 7505.345086 msecs"
"Elapsed time: 4040.289537 msecs"
```

## 13.0.0.hs-adpt

```
"Elapsed time: 3269.578063 msecs"
"Elapsed time: 3820.806803 msecs"
```

## 13.0.0.j9-adpt

```
"Elapsed time: 8063.941225 msecs"
"Elapsed time: 3793.765122 msecs"
```

## 19.2.0-grl

```
"Elapsed time: 11114.87909 msecs"
"Elapsed time: 3935.264804 msecs"
```

## ora 18.9 (build 11.0.5+10-LTS, mixed mode)

```
"Elapsed time: 12387.151908 msecs"
"Elapsed time: 5458.231237 msecs"
```

## ora (build 13.0.1+9, mixed mode, sharing)

```
"Elapsed time: 3528.249572 msecs"
"Elapsed time: 3825.419004 msecs"
```

## 13.0.1-zulu

```
"Elapsed time: 3799.822229 msecs"
"Elapsed time: 3909.198818 msecs"
```

## 13.0.0-librca

```
"Elapsed time: 3617.990272 msecs"
"Elapsed time: 4294.842528 msecs"
```

# Original README...

loading namespaces from user.clj seems have gotten slower on recent
jdks. it is most noticible with macro heavy code (see core.async).

foo.clj loads clojure.core.async then exits. the deps.edn has no
paths, :user alias adds a user.clj on the classpath which loads
foo.clj

clj is the same throughout

```
{:version "1.9.0.375"
 :config-files ["/home/kevin/.clojure/deps.edn" "deps.edn" ]
 :install-dir "/home/kevin/clojure-scripts/lib/clojure"
 :config-dir "/home/kevin/.clojure"
 :cache-dir ".cpcache"
 :force false
 :repro false
 :resolve-aliases ""
 :classpath-aliases ""
 :jvm-aliases ""
 :main-aliases ""
 :all-aliases ""}
```

## Bad

```
openjdk version "12" 2019-03-19
OpenJDK Runtime Environment 19.3 (build 12+30)
OpenJDK 64-Bit Server VM 19.3 (build 12+30, mixed mode, sharing)
```

```
$  clj -A:user                           
"Elapsed time: 18004.782405 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7749.896518 msecs"
```

## Bad

```
openjdk version "11.0.2" 2019-01-15 LTS
OpenJDK Runtime Environment Zulu11.29+3-CA (build 11.0.2+7-LTS)
OpenJDK 64-Bit Server VM Zulu11.29+3-CA (build 11.0.2+7-LTS, mixed mode)
```

```
$ clj -A:user                           
"Elapsed time: 17301.514015 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7875.408021 msecs"
```

## Good

```
openjdk version "1.8.0_192"
OpenJDK Runtime Environment (build 1.8.0_192-b12)
OpenJDK 64-Bit Server VM (build 25.192-b12, mixed mode)
```

```
$ clj -A:user                           
"Elapsed time: 6614.288118 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7434.902931 msecs"
```

## Good

```
openjdk version "1.8.0_72"
OpenJDK Runtime Environment (Zulu 8.13.0.5-linux64) (build 1.8.0_72-b15)
OpenJDK 64-Bit Server VM (Zulu 8.13.0.5-linux64) (build 25.72-b15, mixed mode)
```

```
$ clj -A:user                           
"Elapsed time: 5885.804005 msecs"
```

```
$ clj foo.clj                           
"Elapsed time: 7512.793377 msecs"
```
