# wavesj-docs

### Создаем клиент для ноды тестнета
```java
Node node = new Node(Profile.TESTNET);
```

### Создаем адреса
```java
PrivateKey alice = PrivateKey.fromSeed("some seed 1");
PrivateKey bob = PrivateKey.fromSeed("some seed 2");
```

### IssueTransaction (Builder creation)
```java
// создаем транзакцию создания ассета с названием Asset в количесвте 1000 штук и двумя знаками после запятой
IssueTransaction tx = IssueTransaction.builder("Asset", 1000, 2)
        .getSignedWith(alice); // и подписываем транзакцию приватный ключем Алисы
        
// публикуем транзакцию и дожидаемся пока она положится в блокчейн         
node.waitForTransaction(node.broadcast(tx).id());
//пример созданной транзакции DmpqeTZdXwrxPymZhn9nVBjgnACeXLWyJvriouFaBTc3 на тестнете

// после этого читаем транзакцию из ноды
IssueTransactionInfo txInfo = node.getTransactionInfo(tx.id(), IssueTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("assetId:" + txInfo.tx().assetId().encoded());
System.out.println("name:" + txInfo.tx().name());
System.out.println("quantity:" + txInfo.tx().quantity());
System.out.println("reissuable:" + txInfo.tx().reissuable());
System.out.println("decimals:" + txInfo.tx().decimals());
System.out.println("description:" + txInfo.tx().description());
System.out.println("script:" + txInfo.tx().script().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```
### IssueTransaction (Constructor creation)
```java
// создаем транзакцию
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(), // публичный ключ Алисы
        "Asset", // название ассета
        "description", // описание ассета
        1000, // количество ассета
        2, // количество знаков после запятой
        false, // перевыпускаемость 
        null) // compileScript
        .addProof(alice); // добавляем подпись приватныйм ключом Алисы
        
// публикуем транзакцию и дожидаемся пока она положится в блокчейн         
node.waitForTransaction(node.broadcast(tx).id());
//пример созданной транзакции 7NZ3W2dv8dASFA3oXtHWBRoBWwWuoZb6yUxeDJLADWyu на тестнете

// после этого читаем транзакцию из ноды
IssueTransactionInfo txInfo = node.getTransactionInfo(tx.id(), IssueTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("assetId:" + txInfo.tx().assetId().encoded());
System.out.println("name:" + txInfo.tx().name());
System.out.println("quantity:" + txInfo.tx().quantity());
System.out.println("reissuable:" + txInfo.tx().reissuable());
System.out.println("decimals:" + txInfo.tx().decimals());
System.out.println("description:" + txInfo.tx().description());
System.out.println("script:" + txInfo.tx().script().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Transfer transaction (Builder creation)
```java
// создаем транзакцию
TransferTransaction tx = TransferTransaction
        .builder(
        bob.address(), // указываем получателя
        Amount.of(1000) // указываем количество и ассет, который передаем
        )
        .getSignedWith(alice); // подписываем приватным ключом Алисы

// публикуем и ждем
node.waitForTransaction(node.broadcast(tx).id());

// читаем
TransferTransactionInfo txInfo = node.getTransactionInfo(tx.id(), TransferTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("recipient:" + txInfo.tx().recipient());
System.out.println("assetId:" + txInfo.tx().amount().assetId().encoded());
System.out.println("amount:" + txInfo.tx().amount().value());
System.out.println("attachment:" + txInfo.tx().attachment().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Transfer transaction (Constructor creation)
```java
// создаем транзакцию
TransferTransaction tx = new TransferTransaction(
        alice.publicKey(), // sender public key
        bob.address(), // recipient
        Amount.of(1000), // amount
        null // attachment
        )
        .addProof(alice);

// публикуем и ждем
node.waitForTransaction(node.broadcast(tx).id());

// читаем
TransferTransactionInfo txInfo = node.getTransactionInfo(tx.id(), TransferTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("recipient:" + txInfo.tx().recipient());
System.out.println("assetId:" + txInfo.tx().amount().assetId().encoded());
System.out.println("amount:" + txInfo.tx().amount().value());
System.out.println("attachment:" + txInfo.tx().attachment().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Reissue transaction (Builder creation)
```java
// создаем ассет
AssetId assetId = node.waitForTransaction(node.broadcast(
        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
        IssueTransactionInfo.class)
        .tx().assetId();

// создаем транзакцию довыпуска и подписываем приватным ключем Алисы
ReissueTransaction tx = ReissueTransaction.builder(Amount.of(1000, assetId)).getSignedWith(alice);

// ждем
node.waitForTransaction(node.broadcast(tx).id());

// пример транзакции GSFk5Ziwx33g8KuMyh6wYerxJcHXdcGgXFiBYXH58AE6

// читаем
ReissueTransactionInfo txInfo = node.getTransactionInfo(tx.id(), ReissueTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("assetId:" + txInfo.tx().amount().assetId().encoded());
System.out.println("quantity:" + txInfo.tx().amount().value());
System.out.println("reissuable:" + txInfo.tx().reissuable());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());

```

### Reissue transaction (Constructor creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

ReissueTransaction tx = new ReissueTransaction(
        alice.publicKey(),
        Amount.of(1000, assetId),
        true
).addProof(alice);

// ждем
node.waitForTransaction(node.broadcast(tx).id());

// читаем
ReissueTransactionInfo txInfo = node.getTransactionInfo(tx.id(), ReissueTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("assetId:" + txInfo.tx().amount().assetId().encoded());
System.out.println("quantity:" + txInfo.tx().amount().value());
System.out.println("reissuable:" + txInfo.tx().reissuable());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());

```

### Burn transaction (Builder creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

BurnTransaction tx = BurnTransaction.builder(Amount.of(100, assetId)).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());
// пример транзакции HXnCkfFg9qqYodSygPgkXdyezZiYxao5fVFtKRfphLUY

BurnTransactionInfo txInfo = node.getTransactionInfo(tx.id(), BurnTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("assetId:" + txInfo.tx().amount().assetId().encoded());
System.out.println("amount:" + txInfo.tx().amount().value());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Burn transaction (Constructor creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

BurnTransaction tx = new BurnTransaction(
        alice.publicKey(), 
        new Amount(100, assetId)
).addProof(alice);

node.waitForTransaction(node.broadcast(tx).id());

BurnTransactionInfo txInfo = node.getTransactionInfo(tx.id(), BurnTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("assetId:" + txInfo.tx().amount().assetId().encoded());
System.out.println("amount:" + txInfo.tx().amount().value());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Exchange transaction (Builder creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

Amount amount = Amount.of(1);
Amount price = Amount.of(100, assetId);
long matcherFee = 300000;
Order buy = Order.builder(OrderType.BUY, amount, price, alice.publicKey()).getSignedWith(bob);
Order sell = Order.builder(OrderType.SELL, amount, price, alice.publicKey()).getSignedWith(alice);

ExchangeTransaction tx = ExchangeTransaction
        .builder(buy, sell, amount.value(), price.value(), matcherFee, matcherFee).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

ExchangeTransactionInfo txInfo = node.getTransactionInfo(tx.id(), ExchangeTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());

System.out.println("order1 version:" + txInfo.tx().buyOrder().version());
System.out.println("order1 id:" + txInfo.tx().buyOrder().id());
System.out.println("order1 sender:" + txInfo.tx().buyOrder().sender().address().encoded());
System.out.println("order1 senderPublicKey:" + txInfo.tx().buyOrder().sender().encoded());
System.out.println("order1 matcherPublicKey:" + txInfo.tx().buyOrder().matcher().encoded());
System.out.println("order1 assetPair amountAsset:" + txInfo.tx().buyOrder().assetPair().left().encoded());
System.out.println("order1 assetPair priceAsset:" + txInfo.tx().buyOrder().assetPair().right().encoded());
System.out.println("order1 orderType:" + txInfo.tx().buyOrder().type());
System.out.println("order1 amount:" + txInfo.tx().buyOrder().amount().value());
System.out.println("order1 price:" + txInfo.tx().buyOrder().price().value());
System.out.println("order1 timestamp:" + txInfo.tx().buyOrder().timestamp());
System.out.println("order1 expiration:" + txInfo.tx().buyOrder().expiration());
System.out.println("order1 matcherFee:" + txInfo.tx().buyOrder().fee().value());
System.out.println("order1 signature:" + txInfo.tx().buyOrder().proofs().get(0));
System.out.println("order1 proofs:" + txInfo.tx().buyOrder().proofs().get(0));
System.out.println("order1 matcherFeeAssetId:" + txInfo.tx().buyOrder().fee().assetId().encoded());
System.out.println("order1 eip712Signature:" + Arrays.toString(txInfo.tx().buyOrder().eip712Signature()));

System.out.println("order2 version:" + txInfo.tx().sellOrder().version());
System.out.println("order2 id:" + txInfo.tx().sellOrder().id());
System.out.println("order2 sender:" + txInfo.tx().sellOrder().sender().address().encoded());
System.out.println("order2 senderPublicKey:" + txInfo.tx().sellOrder().sender().encoded());
System.out.println("order2 matcherPublicKey:" + txInfo.tx().sellOrder().matcher().encoded());
System.out.println("order2 assetPair amountAsset:" + txInfo.tx().sellOrder().assetPair().left().encoded());
System.out.println("order2 assetPair priceAsset:" + txInfo.tx().sellOrder().assetPair().right().encoded());
System.out.println("order2 orderType:" + txInfo.tx().sellOrder().type());
System.out.println("order2 amount:" + txInfo.tx().sellOrder().amount().value());
System.out.println("order2 price:" + txInfo.tx().sellOrder().price().value());
System.out.println("order2 timestamp:" + txInfo.tx().sellOrder().timestamp());
System.out.println("order2 expiration:" + txInfo.tx().sellOrder().expiration());
System.out.println("order2 matcherFee:" + txInfo.tx().sellOrder().fee().value());
System.out.println("order2 signature:" + txInfo.tx().sellOrder().proofs().get(0));
System.out.println("order2 proofs:" + txInfo.tx().sellOrder().proofs().get(0));
System.out.println("order2 matcherFeeAssetId:" + txInfo.tx().sellOrder().fee().assetId().encoded());
System.out.println("order2 eip712Signature:" + Arrays.toString(txInfo.tx().sellOrder().eip712Signature()));

System.out.println("amount:" + txInfo.tx().amount());
System.out.println("price:" + txInfo.tx().price());
System.out.println("buyMatcherFee:" + txInfo.tx().buyMatcherFee());
System.out.println("sellMatcherFee:" + txInfo.tx().sellMatcherFee());

System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Exchange transaction (Constructor creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

Amount amount = Amount.of(1);
Amount price = Amount.of(100, assetId);
long matcherFee = 300000;

Order buy = new Order(bob.publicKey(), OrderType.BUY, amount, price, alice.publicKey()).addProof(bob);
Order sell = new Order(alice.publicKey(), OrderType.SELL, amount, price, alice.publicKey()).addProof(alice);

ExchangeTransaction tx = new ExchangeTransaction(
        alice.publicKey(),
        buy,
        sell,
        amount.value(),
        price.value(),
        matcherFee,
        matcherFee
).addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());
        
ExchangeTransactionInfo txInfo = node.getTransactionInfo(tx.id(), ExchangeTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());

System.out.println("order1 version:" + txInfo.tx().buyOrder().version());
System.out.println("order1 id:" + txInfo.tx().buyOrder().id());
System.out.println("order1 sender:" + txInfo.tx().buyOrder().sender().address().encoded());
System.out.println("order1 senderPublicKey:" + txInfo.tx().buyOrder().sender().encoded());
System.out.println("order1 matcherPublicKey:" + txInfo.tx().buyOrder().matcher().encoded());
System.out.println("order1 assetPair amountAsset:" + txInfo.tx().buyOrder().assetPair().left().encoded());
System.out.println("order1 assetPair priceAsset:" + txInfo.tx().buyOrder().assetPair().right().encoded());
System.out.println("order1 orderType:" + txInfo.tx().buyOrder().type());
System.out.println("order1 amount:" + txInfo.tx().buyOrder().amount().value());
System.out.println("order1 price:" + txInfo.tx().buyOrder().price().value());
System.out.println("order1 timestamp:" + txInfo.tx().buyOrder().timestamp());
System.out.println("order1 expiration:" + txInfo.tx().buyOrder().expiration());
System.out.println("order1 matcherFee:" + txInfo.tx().buyOrder().fee().value());
System.out.println("order1 signature:" + txInfo.tx().buyOrder().proofs().get(0));
System.out.println("order1 proofs:" + txInfo.tx().buyOrder().proofs().get(0));
System.out.println("order1 matcherFeeAssetId:" + txInfo.tx().buyOrder().fee().assetId().encoded());
System.out.println("order1 eip712Signature:" + Arrays.toString(txInfo.tx().buyOrder().eip712Signature()));

System.out.println("order2 version:" + txInfo.tx().sellOrder().version());
System.out.println("order2 id:" + txInfo.tx().sellOrder().id());
System.out.println("order2 sender:" + txInfo.tx().sellOrder().sender().address().encoded());
System.out.println("order2 senderPublicKey:" + txInfo.tx().sellOrder().sender().encoded());
System.out.println("order2 matcherPublicKey:" + txInfo.tx().sellOrder().matcher().encoded());
System.out.println("order2 assetPair amountAsset:" + txInfo.tx().sellOrder().assetPair().left().encoded());
System.out.println("order2 assetPair priceAsset:" + txInfo.tx().sellOrder().assetPair().right().encoded());
System.out.println("order2 orderType:" + txInfo.tx().sellOrder().type());
System.out.println("order2 amount:" + txInfo.tx().sellOrder().amount().value());
System.out.println("order2 price:" + txInfo.tx().sellOrder().price().value());
System.out.println("order2 timestamp:" + txInfo.tx().sellOrder().timestamp());
System.out.println("order2 expiration:" + txInfo.tx().sellOrder().expiration());
System.out.println("order2 matcherFee:" + txInfo.tx().sellOrder().fee().value());
System.out.println("order2 signature:" + txInfo.tx().sellOrder().proofs().get(0));
System.out.println("order2 proofs:" + txInfo.tx().sellOrder().proofs().get(0));
System.out.println("order2 matcherFeeAssetId:" + txInfo.tx().sellOrder().fee().assetId().encoded());
System.out.println("order2 eip712Signature:" + Arrays.toString(txInfo.tx().sellOrder().eip712Signature()));

System.out.println("amount:" + txInfo.tx().amount());
System.out.println("price:" + txInfo.tx().price());
System.out.println("buyMatcherFee:" + txInfo.tx().buyMatcherFee());
System.out.println("sellMatcherFee:" + txInfo.tx().sellMatcherFee());

System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Lease transaction (Builder creation)
```java
LeaseTransaction tx = LeaseTransaction.builder(bob.address(), 1000).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

LeaseTransactionInfo txInfo = node.getTransactionInfo(tx.id(), LeaseTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("amount:" + txInfo.tx().amount());
System.out.println("recipient:" + txInfo.tx().recipient().toString());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Lease transaction (Constructor creation)
```java
LeaseTransaction tx = LeaseTransaction tx = new LeaseTransaction(
        alice.publicKey(),
        bob.address(),
        1000
).addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

LeaseTransactionInfo txInfo = node.getTransactionInfo(tx.id(), LeaseTransactionInfo.class);

System.out.println("type:" + txInfo.tx().type());
System.out.println("id:" + txInfo.tx().id());
System.out.println("fee:" + txInfo.tx().fee().value());
System.out.println("feeAssetId:" + txInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + txInfo.tx().timestamp());
System.out.println("version:" + txInfo.tx().version());
System.out.println("chainId:" + txInfo.tx().chainId());
System.out.println("sender:" + txInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + txInfo.tx().sender().encoded());
System.out.println("proofs:" + txInfo.tx().proofs());
System.out.println("amount:" + txInfo.tx().amount());
System.out.println("recipient:" + txInfo.tx().recipient().toString());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```


