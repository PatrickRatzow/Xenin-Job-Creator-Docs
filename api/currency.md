# Currency
All currency related methods & information needed

## addCurrency
```laux
XeninJC.API:addCurrency(ply: Player, amount: number, [ callback: function() ])
```
**Arguments**
1. The target to grant the currency.
2. Amount of currency to be given
3. *[optional]* Callback for when the currency has been given & saved.

## getCurrency
```laux
XeninJC.API:getCurrency(ply: Player): number
```
**Arguments**
1. The target to get the amount of currency from.

## hasCurrency
```laux
XeninJC.API:hasCurrency(ply: Player, amount: number): boolean
```
**Arguments**
1. The target to check from.
2. The amount of currency to check for.

## setCurrency
```laux
XeninJC.API:setCurrency(ply: Player, amount: number, [ callback: function() ])
```
**Arguments**
1. The target to set the currency on.
2. Amount of currency to set to.
3. *[optional]* Callback for when the currency has been set & saved.