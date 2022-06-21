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

