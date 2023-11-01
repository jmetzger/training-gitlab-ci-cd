# Wann ist eine Pipeline langsam 

## Repo ist sehr gross

  * was kann ich tun: depth niedriger setzen, statt 20
  * Brauche ich das Repo in dem Job ?-> ansonsten GIT_STRATEGY: none 

## Image ist zu gross 

  * Image verschlanken, wenn es keine Standard-Image ist, im Image-Bauprozes

## Caching 

  * Wenn caching verwendet und wenn ja richtig ?

## Scheduling in der Pipelines 

  * sehr lange Laufzeiten, weil einzelne Stages sehr lange brauchen (standardverhalten: jeder Stage muss komplett fertig sein, damit der nächste Stage starten kann)
  * Lösung: Acyclice Pipelines: z.B. build_a -> test_a -> deploy_a kann parallel laufen zu build_b -> test_b -> deploy_b

