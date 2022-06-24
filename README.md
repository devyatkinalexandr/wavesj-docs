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
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(),
        "Asset",
        "",
        1000,
        2,
        true,
        Base64String.empty())
        .addProof(alice);
AssetId assetId = node.waitForTransaction(node.broadcast(tx).id(), IssueTransactionInfo.class).tx().assetId();

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
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(),
        "Asset",
        "",
        1000,
        2,
        true,
        Base64String.empty())
        .addProof(alice);
AssetId assetId = node.waitForTransaction(node.broadcast(tx).id(), IssueTransactionInfo.class).tx().assetId();

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
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(),
        "Asset",
        "",
        1000,
        2,
        true,
        Base64String.empty())
        .addProof(alice);
AssetId assetId = node.waitForTransaction(node.broadcast(tx).id(), IssueTransactionInfo.class).tx().assetId();

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

### Lease cancel transaction (Builder creation)
```java
long amount = 1000;

LeaseTransaction leaseTx = LeaseTransaction.builder(bob.address(), amount).getSignedWith(alice);
int leaseHeight = node.waitForTransaction(node.broadcast(leaseTx).id()).height();

LeaseCancelTransaction tx = LeaseCancelTransaction.builder(leaseTx.id()).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
LeaseCancelTransactionInfo txInfo = node.getTransactionInfo(tx.id(), LeaseCancelTransactionInfo.class);

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
System.out.println("leaseId:" + txInfo.tx().leaseId().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
System.out.println("lease id:" + txInfo.leaseInfo().id().encoded());
System.out.println("lease originTransactionId:" + txInfo.leaseInfo().originTransactionId().encoded());
System.out.println("lease sender:" + txInfo.leaseInfo().sender().encoded());
System.out.println("lease recipient:" + txInfo.leaseInfo().recipient().toString());
System.out.println("lease recipient:" + txInfo.leaseInfo().recipient().toString());
System.out.println("lease amount:" + txInfo.leaseInfo().amount());
System.out.println("lease height:" + txInfo.leaseInfo().height());
System.out.println("lease status:" + txInfo.leaseInfo().status().toString());
System.out.println("lease cancelHeight:" + txInfo.leaseInfo().cancelHeight().getAsInt());
System.out.println("lease cancelTransactionId:" + txInfo.leaseInfo().cancelTransactionId().get().encoded());
```

### Lease cancel transaction (Constructor creation)
```java
long amount = 1000;

LeaseTransaction leaseTx = new LeaseTransaction(alice.publicKey(), bob.address(), amount).addProof(alice);
int leaseHeight = node.waitForTransaction(node.broadcast(leaseTx).id()).height();

LeaseCancelTransaction tx = new LeaseCancelTransaction(alice.publicKey(), leaseTx.id()).addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
LeaseCancelTransactionInfo txInfo = node.getTransactionInfo(tx.id(), LeaseCancelTransactionInfo.class);

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
System.out.println("leaseId:" + txInfo.tx().leaseId().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
System.out.println("lease id:" + txInfo.leaseInfo().id().encoded());
System.out.println("lease originTransactionId:" + txInfo.leaseInfo().originTransactionId().encoded());
System.out.println("lease sender:" + txInfo.leaseInfo().sender().encoded());
System.out.println("lease recipient:" + txInfo.leaseInfo().recipient().toString());
System.out.println("lease recipient:" + txInfo.leaseInfo().recipient().toString());
System.out.println("lease amount:" + txInfo.leaseInfo().amount());
System.out.println("lease height:" + txInfo.leaseInfo().height());
System.out.println("lease status:" + txInfo.leaseInfo().status().toString());
System.out.println("lease cancelHeight:" + txInfo.leaseInfo().cancelHeight().getAsInt());
System.out.println("lease cancelTransactionId:" + txInfo.leaseInfo().cancelTransactionId().get().encoded());
```

### Create alias transaction (Builder creation)
```java
Alias alias = Alias.as("alice_" + System.currentTimeMillis());

CreateAliasTransaction tx = CreateAliasTransaction.builder(alias.toString()).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
CreateAliasTransactionInfo txInfo = node.getTransactionInfo(tx.id(), CreateAliasTransactionInfo.class);

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
System.out.println("alias:" + txInfo.tx().alias().toString());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Create alias transaction (Constructor creation)
```java
Alias alias = Alias.as("alice_" + System.currentTimeMillis());
        
CreateAliasTransaction tx = new CreateAliasTransaction(alice.publicKey(), alias.toString()).addProof(alice);;
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
CreateAliasTransactionInfo txInfo = node.getTransactionInfo(tx.id(), CreateAliasTransactionInfo.class);

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
System.out.println("alias:" + txInfo.tx().alias().toString());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Mass transfer transaction (Builder creation)
```java
MassTransferTransaction tx = MassTransferTransaction.builder(Transfer.to(bob.address(), 1000)).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
MassTransferTransactionInfo txInfo = node.getTransactionInfo(tx.id(), MassTransferTransactionInfo.class);

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
System.out.println("attachment:" + txInfo.tx().attachment().encoded());
System.out.println("transferCount:" + txInfo.tx().transfers().size());
System.out.println("totalAmount:" + txInfo.tx().total());
System.out.println("transfers recipient:" + txInfo.tx().transfers().get(0).recipient().toString());
System.out.println("transfers amount:" + txInfo.tx().transfers().get(0).amount());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Mass transfer transaction (Constructor creation)
```java
MassTransferTransaction tx = new MassTransferTransaction(
                alice.publicKey(),
                AssetId.WAVES,
                Collections.singletonList(Transfer.to(bob.address(), 1000)),
                null)
                .addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
MassTransferTransactionInfo txInfo = node.getTransactionInfo(tx.id(), MassTransferTransactionInfo.class);

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
System.out.println("attachment:" + txInfo.tx().attachment().encoded());
System.out.println("transferCount:" + txInfo.tx().transfers().size());
System.out.println("totalAmount:" + txInfo.tx().total());
System.out.println("transfers recipient:" + txInfo.tx().transfers().get(0).recipient().toString());
System.out.println("transfers amount:" + txInfo.tx().transfers().get(0).amount());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Data transaction (Builder creation)
```java
DataTransaction tx = DataTransaction.builder(StringEntry.as("str", alice.address().toString())).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
DataTransactionInfo txInfo = node.getTransactionInfo(tx.id(), DataTransactionInfo.class);

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
System.out.println("data key:" + txInfo.tx().data().get(0).key());
System.out.println("data type:" + txInfo.tx().data().get(0).type().name());
System.out.println("data value:" + txInfo.tx().data().get(0).valueAsObject());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Data transaction (Constructor creation)
```java
DataTransaction tx = new DataTransaction(
                alice.publicKey(), 
                Collections.singletonList(StringEntry.as("str", alice.address().encoded()))
).addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
DataTransactionInfo txInfo = node.getTransactionInfo(tx.id(), DataTransactionInfo.class);

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
System.out.println("data key:" + txInfo.tx().data().get(0).key());
System.out.println("data type:" + txInfo.tx().data().get(0).type().name());
System.out.println("data value:" + txInfo.tx().data().get(0).valueAsObject());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Sponsor fee transaction (Builder creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

SponsorFeeTransaction tx = SponsorFeeTransaction.builder(assetId, 5).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
SponsorFeeTransactionInfo txInfo = node.getTransactionInfo(tx.id(), SponsorFeeTransactionInfo.class);

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
System.out.println("minSponsoredAssetFee:" + txInfo.tx().minSponsoredFee());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Sponsor fee transaction (Constructor creation)
```java
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(),
        "Asset",
        "",
        1000,
        2,
        true,
        Base64String.empty())
        .addProof(alice);
AssetId assetId = node.waitForTransaction(node.broadcast(tx).id(), IssueTransactionInfo.class).tx().assetId();
        
SponsorFeeTransaction tx = new SponsorFeeTransaction(alice.publicKey(), assetId, 5).addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
SponsorFeeTransactionInfo txInfo = node.getTransactionInfo(tx.id(), SponsorFeeTransactionInfo.class);

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
System.out.println("minSponsoredAssetFee:" + txInfo.tx().minSponsoredFee());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Set asset script (Builder creation)
```java
Base64String script = node.compileScript("{-# SCRIPT_TYPE ASSET #-} true").script();
        AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2)
                                .script(script).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

SetAssetScriptTransaction tx = SetAssetScriptTransaction.builder(assetId, script).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
SetAssetScriptTransactionInfo txInfo = node.getTransactionInfo(tx.id(), SetAssetScriptTransactionInfo.class);

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
System.out.println("script:" + txInfo.tx().script().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Set asset script (Constructor creation)
```java
Base64String script = node.compileScript("{-# SCRIPT_TYPE ASSET #-} true").script();
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(),
        "Asset",
        "",
        1000,
        2,
        true,
        Base64String.empty()
        )
        .addProof(alice);
AssetId assetId = node.waitForTransaction(node.broadcast(tx).id(), IssueTransactionInfo.class).tx().assetId();

        
SetAssetScriptTransaction tx = new SetAssetScriptTransaction(alice.publicKey(), assetId, script).addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

TransactionInfo commonInfo = node.getTransactionInfo(tx.id());
SetAssetScriptTransactionInfo txInfo = node.getTransactionInfo(tx.id(), SetAssetScriptTransactionInfo.class);

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
System.out.println("script:" + txInfo.tx().script().encoded());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Invoke script transaction (Builder creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
        IssueTransactionInfo.class).tx().assetId();

Base64String script = node.compileScript(
        "{-# STDLIB_VERSION 5 #-}\n" +
        "{-# CONTENT_TYPE DAPP #-}\n" +
        "{-# SCRIPT_TYPE ACCOUNT #-}\n" +
        "@Callable(inv)\n" +
        "func call(bv: ByteVector, b: Boolean, int: Int, str: String, list: List[Int]) = {\n" +
        "  let asset = Issue(\"Asset\", \"\", 1, 0, true)\n" +
        "  let assetId = asset.calculateAssetId()\n" +
        "  let lease = Lease(inv.caller, 7)\n" +
        "  let leaseId = lease.calculateLeaseId()\n" +
        "  [\n" +
        "    BinaryEntry(\"bin\", assetId),\n" +
        "    BooleanEntry(\"bool\", true),\n" +
        "    IntegerEntry(\"int\", 100500),\n" +
        "    StringEntry(\"assetId\", assetId.toBase58String()),\n" +
        "    StringEntry(\"leaseId\", leaseId.toBase58String()),\n" +
        "    StringEntry(\"del\", \"\"),\n" +
        "    DeleteEntry(\"del\"),\n" +
        "    asset,\n" +
        "    SponsorFee(assetId, 1),\n" +
        "    Reissue(assetId, 4, false),\n" +
        "    Burn(assetId, 3),\n" +
        "    ScriptTransfer(inv.caller, 2, assetId),\n" +
        "    lease,\n" +
        "    LeaseCancel(lease.calculateLeaseId())\n" +
        "  ]\n" +
        "}").script();
node.waitForTransaction(node.broadcast(SetScriptTransaction.builder(script).getSignedWith(bob)).id());

InvokeScriptTransaction tx = InvokeScriptTransaction
        .builder(bob.address(), Function.as("call",
        BinaryArg.as(alice.address().bytes()),
        BooleanArg.as(true),
        IntegerArg.as(100500),
        StringArg.as(alice.address().toString()),
        ListArg.as(IntegerArg.as(100500))
        ))
        .payments(
            Amount.of(1, assetId),
            Amount.of(2, assetId),
            Amount.of(3, assetId),
            Amount.of(4, assetId),
            Amount.of(5, assetId),
            Amount.of(6, assetId),
            Amount.of(7, assetId),
            Amount.of(8, assetId),
            Amount.of(9, assetId),
            Amount.of(10, assetId)
        )
        .extraFee(1_00000000)
        .getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

InvokeScriptTransactionInfo txInfo = node.getTransactionInfo(
        new Id("68qf34fyrKSRWP95kaLnS1kysLJKXuM14E1qtr3WAky7"),
        InvokeScriptTransactionInfo.class
);

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
System.out.println("dApp:" + txInfo.tx().dApp().toString());
System.out.println("payment:" + txInfo.tx().payments());
System.out.println("call function:" + txInfo.tx().function().name());
System.out.println("call args:" + txInfo.tx().function().args());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
System.out.println("state changes:" + txInfo.stateChanges().toString());
```

### Invoke script transaction (Constructor creation)
```java
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(),
        "Asset",
        "",
        1000,
        2,
        true,
        Base64String.empty())
        .addProof(alice);
AssetId assetId = node.waitForTransaction(node.broadcast(tx).id(), IssueTransactionInfo.class).tx().assetId();

Base64String script = node.compileScript(
        "{-# STDLIB_VERSION 5 #-}\n" +
        "{-# CONTENT_TYPE DAPP #-}\n" +
        "{-# SCRIPT_TYPE ACCOUNT #-}\n" +
        "@Callable(inv)\n" +
        "func call(bv: ByteVector, b: Boolean, int: Int, str: String, list: List[Int]) = {\n" +
        "  let asset = Issue(\"Asset\", \"\", 1, 0, true)\n" +
        "  let assetId = asset.calculateAssetId()\n" +
        "  let lease = Lease(inv.caller, 7)\n" +
        "  let leaseId = lease.calculateLeaseId()\n" +
        "  [\n" +
        "    BinaryEntry(\"bin\", assetId),\n" +
        "    BooleanEntry(\"bool\", true),\n" +
        "    IntegerEntry(\"int\", 100500),\n" +
        "    StringEntry(\"assetId\", assetId.toBase58String()),\n" +
        "    StringEntry(\"leaseId\", leaseId.toBase58String()),\n" +
        "    StringEntry(\"del\", \"\"),\n" +
        "    DeleteEntry(\"del\"),\n" +
        "    asset,\n" +
        "    SponsorFee(assetId, 1),\n" +
        "    Reissue(assetId, 4, false),\n" +
        "    Burn(assetId, 3),\n" +
        "    ScriptTransfer(inv.caller, 2, assetId),\n" +
        "    lease,\n" +
        "    LeaseCancel(lease.calculateLeaseId())\n" +
        "  ]\n" +
        "}").script();

node.waitForTransaction(node.broadcast(new SetScriptTransaction(bob.publicKey(), script).addProof(bob)).id());

ArrayList<Amount> payments = new ArrayList<>();
payments.add(Amount.of(1, assetId));
payments.add(Amount.of(2, assetId));
payments.add(Amount.of(3, assetId));
payments.add(Amount.of(4, assetId));
payments.add(Amount.of(5, assetId));
payments.add(Amount.of(6, assetId));
payments.add(Amount.of(7, assetId));
payments.add(Amount.of(8, assetId));
payments.add(Amount.of(9, assetId));
payments.add(Amount.of(10, assetId));

InvokeScriptTransaction tx = new InvokeScriptTransaction(
        alice.publicKey(),
        bob.address(),
        Function.as("call",
                BinaryArg.as(alice.address().bytes()),
                BooleanArg.as(true),
                IntegerArg.as(100500),
                StringArg.as(alice.address().toString()),
                ListArg.as(IntegerArg.as(100500))
        ),
        payments
)
        .addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

InvokeScriptTransactionInfo txInfo = node.getTransactionInfo(
        new Id("68qf34fyrKSRWP95kaLnS1kysLJKXuM14E1qtr3WAky7"),
        InvokeScriptTransactionInfo.class
);

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
System.out.println("dApp:" + txInfo.tx().dApp().toString());
System.out.println("payment:" + txInfo.tx().payments());
System.out.println("call function:" + txInfo.tx().function().name());
System.out.println("call args:" + txInfo.tx().function().args());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
System.out.println("state changes:" + txInfo.stateChanges().toString());
```

### Update asset info transaction (Builder creation)
```java
AssetId assetId = node.waitForTransaction(node.broadcast(
                        IssueTransaction.builder("Asset", 1000, 2).getSignedWith(alice)).id(),
                IssueTransactionInfo.class).tx().assetId();

node.waitBlocks(2);

UpdateAssetInfoTransaction tx = UpdateAssetInfoTransaction
                .builder(assetId, "New Asset", "New description").getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

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
System.out.println("description:" + txInfo.tx().description());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Update asset info transaction (Constructor creation)
```java
IssueTransaction tx = new IssueTransaction(
        alice.publicKey(),
        "Asset",
        "",
        1000,
        2,
        true,
        Base64String.empty())
        .addProof(alice);
AssetId assetId = node.waitForTransaction(node.broadcast(tx).id(), IssueTransactionInfo.class).tx().assetId();

node.waitBlocks(2);
        
UpdateAssetInfoTransaction tx = new UpdateAssetInfoTransaction(
        alice.publicKey(), 
        assetId, 
        "New Asset", 
        "New description"
).addProof(alice);
node.waitForTransaction(node.broadcast(tx).id());

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
System.out.println("description:" + txInfo.tx().description());
System.out.println("height:" + txInfo.height());
System.out.println("applicationStatus:" + txInfo.applicationStatus());
```

### Ethereum transfer transaction
```java
Credentials charlie = MetamaskHelper.generateCredentials("some mnemonic");
String charlieAddress = WavesEthConverter.ethToWavesAddress(charlie.getAddress(), ChainId.TESTNET);

TransferTransaction tx = TransferTransaction.builder(new Address(charlieAddress), Amount.of(1_00_000_000)).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

EthereumTransaction transferTx = EthereumTransaction.createAndSign(
        new EthereumTransaction.Transfer(
                new Address(alice.address().encoded()),
                new Amount(1000, AssetId.WAVES)
        ),
        DEFAULT_GAS_PRICE,
        WavesConfig.chainId(),
        100000L,
        Instant.now().toEpochMilli(),
        charlie.getEcKeyPair()
);

EthRpcResponse rs = node.broadcastEthTransaction(transferTx);
node.waitForTransaction(transferTx.id());
EthereumTransactionInfo ethTxInfo = node.getTransactionInfo(transferTx.id(), EthereumTransactionInfo.class);

EthereumTransaction.Transfer payload = (EthereumTransaction.Transfer) ethTxInfo.tx().payload();

System.out.println("isTransfer transaction:" + ethTxInfo.isTransferTransaction());
System.out.println("type:" + ethTxInfo.tx().type());
System.out.println("id:" + ethTxInfo.tx().id());
System.out.println("fee:" + ethTxInfo.tx().fee().value());
System.out.println("feeAssetId:" + ethTxInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + ethTxInfo.tx().timestamp());
System.out.println("version:" + ethTxInfo.tx().version());
System.out.println("chainId:" + ethTxInfo.tx().chainId());
System.out.println("sender:" + ethTxInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + ethTxInfo.tx().sender().encoded());
System.out.println("proofs:" + ethTxInfo.tx().proofs());
System.out.println("payload recipient:" + payload.recipient().encoded());
System.out.println("payload asset:" + payload.amount().assetId().encoded());
System.out.println("payload amount:" + payload.amount().value());
System.out.println("asset:" + payload.amount().assetId().encoded());
System.out.println("height:" + ethTxInfo.height());
System.out.println("applicationStatus:" + ethTxInfo.applicationStatus());
```

### Ethereum invoke script transaction
```java
Credentials charlie = MetamaskHelper.generateCredentials("some mnemonic");
String charlieAddress = WavesEthConverter.ethToWavesAddress(charlie.getAddress(), ChainId.TESTNET);
        
Base64String script = node.compileScript(
        "{-# STDLIB_VERSION 5 #-}\n" +
        "{-# CONTENT_TYPE DAPP #-}\n" +
        "{-# SCRIPT_TYPE ACCOUNT #-}\n" +
        "@Callable(inv)\n" +
        "func call(bv: ByteVector, b: Boolean, int: Int, str: String, list: List[Int]) = {\n" +
        "  let asset = Issue(\"Asset\", \"\", 1, 0, true)\n" +
        "  let assetId = asset.calculateAssetId()\n" +
        "  let lease = Lease(inv.caller, 7)\n" +
        "  let leaseId = lease.calculateLeaseId()\n" +
        "  [\n" +
        "    BinaryEntry(\"bin\", assetId),\n" +
        "    BooleanEntry(\"bool\", true),\n" +
        "    IntegerEntry(\"int\", 100500),\n" +
        "    StringEntry(\"assetId\", assetId.toBase58String()),\n" +
        "    StringEntry(\"leaseId\", leaseId.toBase58String()),\n" +
        "    StringEntry(\"del\", \"\"),\n" +
        "    DeleteEntry(\"del\"),\n" +
        "    asset,\n" +
        "    SponsorFee(assetId, 1),\n" +
        "    Reissue(assetId, 4, false),\n" +
        "    Burn(assetId, 3),\n" +
        "    ScriptTransfer(inv.caller, 2, assetId),\n" +
        "    lease,\n" +
        "    LeaseCancel(lease.calculateLeaseId())\n" +
        "  ]\n" +
        "}").script();

node.waitForTransaction(node.broadcast(SetScriptTransaction.builder(script).fee(3400000).getSignedWith(alice)).id());

TransferTransaction tx = TransferTransaction.builder(
        new Address(charlieAddress), Amount.of(1_00_000_000)).getSignedWith(alice);
node.waitForTransaction(node.broadcast(tx).id());

ArrayList<Amount> payments = new ArrayList<>();
payments.add(Amount.of(1, AssetId.WAVES));
payments.add(Amount.of(2, AssetId.WAVES));
payments.add(Amount.of(3, AssetId.WAVES));

EthereumTransaction ethInvokeTx = EthereumTransaction.createAndSign(
        new EthereumTransaction.Invocation(
                alice.address(),
                Function.as("call",
                            BinaryArg.as(new Address(charlieAddress).bytes()),
                            BooleanArg.as(true),
                            IntegerArg.as(100500),
                            StringArg.as(alice.address().toString()),
                            ListArg.as(IntegerArg.as(100500))
                ),
                        payments
                ),
        DEFAULT_GAS_PRICE,
        WavesConfig.chainId(),
        100500000L,
        Instant.now().toEpochMilli(),
        charlie.getEcKeyPair()
);

EthRpcResponse rs = node.broadcastEthTransaction(ethInvokeTx);
node.waitForTransaction(ethInvokeTx.id());

EthereumTransactionInfo ethInvokeTxInfo = node.getTransactionInfo(ethInvokeTx.id(), EthereumTransactionInfo.class);

System.out.println("isInvocation:" + ethInvokeTxInfo.isInvokeTransaction());
System.out.println("type:" + ethInvokeTxInfo.tx().type());
System.out.println("id:" + ethInvokeTxInfo.tx().id());
System.out.println("fee:" + ethInvokeTxInfo.tx().fee().value());
System.out.println("feeAssetId:" + ethInvokeTxInfo.tx().fee().assetId().encoded());
System.out.println("timestamp:" + ethInvokeTxInfo.tx().timestamp());
System.out.println("version:" + ethInvokeTxInfo.tx().version());
System.out.println("chainId:" + ethInvokeTxInfo.tx().chainId());
System.out.println("sender:" + ethInvokeTxInfo.tx().sender().address().encoded());
System.out.println("senderPublicKey:" + ethInvokeTxInfo.tx().sender().encoded());
System.out.println("proofs:" + ethInvokeTxInfo.tx().proofs());
System.out.println("payload dApp:" + invocation.dApp().encoded());
System.out.println("payload call function:" + invocation.function().name());
System.out.println("payload call args:" + invocation.function().args());
System.out.println("payment:" + invocation.payments());
System.out.println("stateChanges:" + ethInvokeTxInfo.getStateChanges());
System.out.println("height:" + ethInvokeTxInfo.height());
System.out.println("applicationStatus:" + ethInvokeTxInfo.applicationStatus());
```




