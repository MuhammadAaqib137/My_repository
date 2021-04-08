---
id: litvis

narrative-schemas:
  - ../../narrative-schemas/project.yml

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest
---

@import "../../css/datavis.less"

```elm {l=hidden}
import Tidy exposing (..)
import VegaLite exposing (..)
```

```elm {l v interactive}
myBarchart : Spec
myBarchart =
    let
        data =
            dataFromUrl "https://raw.githubusercontent.com/aliaa122/datasets/main/month_count.csv" []

        enc =
            encoding
                << position X [ pName "Month", pTemporal ]
                << position Y [ pName "Count", pQuant ]
                << tooltips
                    [ [ tName "Month", tTemporal, tFormat "%B %Y" ]
                    , [ tName "Count", tTitle "Count" ]
                    ]
    in
    toVegaLite [ width 600, data, enc [], bar [] ]
```

```elm {l v interactive}
myBarchart2 : Spec
myBarchart2 =
    let
        data =
            dataFromUrl "https://raw.githubusercontent.com/aliaa122/datasets/main/day_count.csv" []

        enc =
            encoding
                << position X [ pName "Trading day", pTemporal ]
                << position Y [ pName "Trading Activity", pQuant ]
                << tooltips
                    [ [ tName "Trading day", tTemporal ]
                    , [ tName "Trading Activity" ]
                    ]

    in
    toVegaLite [ width 600, data, enc [], bar [] ]
```

```elm {l v interactive}
euChart : Spec
euChart =
    let
        data =
            dataFromUrl "https://raw.githubusercontent.com/aliaa122/datasets/main/execution_pct.csv" []

        enc =
            encoding
                << position X [ pName "Trading day", pTemporal ]
                << position Y [ pName "Percent", pQuant ]
                -- << color [ mName "Type" ]
                << color
                  [ mName "Type"
                --   , mScale
                --       (categoricalDomainMap
                --           [ ( "Buy", "rgb(49,148,247)" )
                --           , ( "Sell", "rgb(247,0,0)" )
                --           ]
                --       )
                  ]
                << tooltips
                [ [ tName "Trading day", tTemporal ]
                , [ tName "Percent", tTitle "Percent" ]
                --, [ tName "Buy", tTitle "Buy Executions" ]
                --, [ tName "Sell", tTitle "Sell Executions" ]
                ]
    in
    toVegaLite [ width 600, data, enc [], bar [] ]
```

```elm {l v}
euChart2 : Spec
euChart2 =
    let
        data =
            dataFromUrl "https://raw.githubusercontent.com/aliaa122/datasets/main/execution_pct.csv" []

        enc =
            encoding
                << position X [ pName "Trading day", pTemporal ]
                << position Y [ pName "Percent", pQuant ]
                << color [ mName "Type" ]
    in
    toVegaLite [ width 600, data, enc [], area [] ]
```

