### 建议您先阅读官方文档

Coinbase 文档地址 [https://docs.pro.coinbase.com](https://docs.pro.coinbase.com)

所有接口方法的初始化都与coinbase提供的方法相同。更多细节 [src/api](https://github.com/zhouaini528/coinbase-php/tree/master/src/Api)

大部分的接口已经完成，使用者可以根据我的设计方案继续扩展，欢迎与我一起迭代它。

[English Document](https://github.com/zhouaini528/coinbase-php/blob/master/README.md)

### 其他交易所API

[Exchanges](https://github.com/zhouaini528/exchanges-php) 它包含以下所有交易所，强烈推荐使用该SDK。

[Bitmex](https://github.com/zhouaini528/bitmex-php)

[Okex](https://github.com/zhouaini528/okex-php)

[Huobi](https://github.com/zhouaini528/huobi-php)

[Binance](https://github.com/zhouaini528/binance-php)

[Kucoin](https://github.com/zhouaini528/Kucoin-php)

[Mxc](https://github.com/zhouaini528/mxc-php)

[Coinbase](https://github.com/zhouaini528/coinbase-php)

[ZB](https://github.com/zhouaini528/zb-php)

[Bitfinex](https://github.com/zhouaini528/zb-php)

[Bittrex](https://github.com/zhouaini528/bittrex-php)

[Gate](https://github.com/zhouaini528/gate-php)

#### 安装方式
```
composer require linwj/coinbase
```

支持更多的请求设置
```php
$coinbase=new Coinbase();

//You can set special needs
$coinbase->setOptions([
    //Set the request timeout to 60 seconds by default
    'timeout'=>10,
    
    //If you are developing locally and need an agent, you can set this
    'proxy'=>true,
    //More flexible Settings
    /* 'proxy'=>[
     'http'  => 'http://127.0.0.1:12333',
     'https' => 'http://127.0.0.1:12333',
     'no'    =>  ['.cn']
     ], */
    //Close the certificate
    //'verify'=>false,
]);
```

### 现货交易 API

Market related API [More](https://github.com/zhouaini528/coinbase-php/blob/master/tests/product.php)
```php
$coinbase=new Coinbase();

try {
    $result=$coinbase->product()->getList();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$coinbase->product()->getBook([
        'product_id'=>'BTC-USD',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$coinbase->product()->getCandles([
        'product_id'=>'BTC-USD',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

```

Order related API [More](https://github.com/zhouaini528/coinbase-php/blob/master/tests/order.php)
```php
$coinbase=new Coinbase($key,$secret);

//****************************LIMIT
try {
    $result=$coinbase->order()->post([
        //'client_oid'=>'',
        'type'=>'limit',
        'side'=>'sell',
        'product_id'=>'BTC-USD',
        'price'=>'20000',
        'size'=>'0.01'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
sleep(1);

//track the order
try {
    $result=$coinbase->order()->get([
        'id'=>$result['id'],
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
sleep(1);

//cancellation of order
try {
    $result=$coinbase->order()->delete([
        'id'=>$result['id'],
        //'id'=>'6bad6a7d-b01a-4a93-9e6e-e9934bcef4ef',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

//****************************MARKET
try {
    $result=$coinbase->order()->post([
        //'client_oid'=>'',
        'type'=>'market',
        'side'=>'sell',
        'product_id'=>'BTC-USD',
        'size'=>'0.01',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
sleep(1);

//track the order
try {
    $result=$coinbase->order()->get([
        'id'=>$result['id'],
        //'client_oid'=>''
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```

Accounts related API [More]()
```php
$coinbase=new Coinbase($key,$secret);

try {
    $result=$coinbase->account()->getList();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$coinbase->account()->get([
        'account_id'=>'c74a36f5-4f2b-495b-be29-6eb2458d1b3a'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$coinbase->account()->getHolds([
        'account_id'=>'c74a36f5-4f2b-495b-be29-6eb2458d1b3a'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$coinbase->account()->getLedger([
        'account_id'=>'c74a36f5-4f2b-495b-be29-6eb2458d1b3a'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

```

[更多用例](https://github.com/zhouaini528/coinbase-php/tree/master/tests)

[更多API](https://github.com/zhouaini528/coinbase-php/tree/master/src/Api)