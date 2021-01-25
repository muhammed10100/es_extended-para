# es_extended-para

es_extended\server\lasses\player.lua 27.satırından aşağıdaki kodu bulunuz.
```
self.getMoney = function()
    return self.player.get('money')
end
```
Bu kodu aşağıdaki kod ile değiştiriniz.
```
self.getMoney = function()
    local money = self.getInventoryItem('cash')
    
    if self.player.get('money') ~= money.count then
        self.player.set('money',money.count)
    end
    return money.count
end
```

es_extended\server\lasses\player.lua 65.satırından aşağıdaki kodu bulunuz.
```
self.addMoney = function(money)
    money = ESX.Math.Round(money)
    if money >= 0 then
        self.player.addMoney(money)
    else
        print(('es_extended: %s attempted exploiting! (reason: player tried adding -1 cash balance)'):format(self.identifier))
        end
    end
    self.removeMoney = function(money)
        money = ESX.Math.Round(money)
    if money >= 0 then
        self.player.removeMoney(money)
    else
        print(('es_extended: %s attempted exploiting! (reason: player tried removing -1 cash balance)'):format(self.identifier))
    end
end
```
Bu kodu aşağıdaki kod ile değiştir.
```
self.addMoney = function(money)
    money = ESX.Math.Round(money)
    if money >= 0 then
        self.addInventoryItem("cash",money)
    local money = self.getInventoryItem('cash')
    if self.player.get('money') ~= money.count then
        self.player.set('money',money.count)
    end
    else
        print(('es_extended: %s attempted exploiting! (reason: player tried adding -1 cash balance)'):format(self.identifier))
        end
    end
    self.removeMoney = function(money)
        money = ESX.Math.Round(money)
    if money >= 0 then
        self.removeInventoryItem("cash",money)
    local money = self.getInventoryItem('cash')
    
    if self.player.get('money') ~= money.count then
        self.player.set('money',money.count)
    end
    else
        print(('es_extended: %s attempted exploiting! (reason: player tried removing -1 cash balance)'):format(self.identifier))
    end
end
```
