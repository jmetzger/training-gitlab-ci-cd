# Variablen in Pipeline - Formular anzeigen 

## So wird es nicht angezeigt:

```
variables:
  MAX_PERFORMANCE: 'true'
```

## So wird es angezeigt:

```

variables:
   MAX_PERFORMANCE: 
     description: Decide if to run max_performance 'true' or 'false'
     value: 'false'
```

![image](https://github.com/jmetzger/training-gitlab-ci-cd/assets/1933318/8047c095-6d99-4576-b86a-fa6ba0953e47)

## Mit Optionen 

### So hinterlegen 

```
variables:
   MAX_PERFORMANCE: 
     description: Decide if to run max_performance 'true' or 'false'
     value: 'false'
     options:
       - 'false'
       - 'true'

```
