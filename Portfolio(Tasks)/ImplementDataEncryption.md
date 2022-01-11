---
layout: page
title: Implement data encryption
parent: Tasks
permalink: /tasks13/
nav_order: 13
---
<a name="Implementdataencryption"></a>
# Implement data encryption 

In this part, I will encrypt and decrypt data using Java language. The following sample Java program shows how to encrypt data using AES encryption algorithm. Java provides a number of helper classes for AES encryption such as Cipher (for encryption/decryption), SecretKey (represents the shared secret key) and KeyGenerator (generates the shared secret key).

Figure 1 shows the process of encrypting data. To encrypt data, we need a secret key and plain text, and we will write a method to encrypt the plain text. As results, we will the cipher text, which is the encrypted text.

![No alt text provided for this
image](../myMediaFolder/media/security-aes_design_mobile.jpg)

**Figure 1**


<b></b>

## 1. ECB mode

The following parameters are needed in order to decrypt and encrypt text, as I mentioned before.
```
        String plainText = "Cyber security minor || S7";
        SecretKey secKey = getSecretEncryptionKey();
        byte[] cipherText = encryptText(plainText, secKey);
        String decryptedText = decryptText(cipherText, secKey);

```
<b></b>


The following method will generate secret key that will use soon to encrypt and decrypt data.

```
    public static SecretKey getSecretEncryptionKey() throws Exception{
        KeyGenerator generator = KeyGenerator.getInstance("AES");
        generator.init(128); // The AES key size in number of bits
        SecretKey secKey = generator.generateKey();
        return secKey;
    }
```

<b></b>


The following method is used to encrypt data. The method will return encrypted data as a list of bytes. The method required the secret key and the plain text.

```
    public static byte[] encryptText(String plainText,SecretKey secKey) throws Exception{
        Cipher aesCipher = Cipher.getInstance("AES");
        aesCipher.init(Cipher.ENCRYPT_MODE, secKey);
        byte[] byteCipherText = aesCipher.doFinal(plainText.getBytes());
        return byteCipherText;
    }
```

<b></b>

The following method is used to decrypt data. The method will return decrypt data as string. The method required the secret key and a list of bytes (encrypted text).

```
    public static String decryptText(byte[] byteCipherText, SecretKey secKey) throws Exception {
        Cipher aesCipher = Cipher.getInstance("AES");
        aesCipher.init(Cipher.DECRYPT_MODE, secKey);
        byte[] bytePlainText = aesCipher.doFinal(byteCipherText);
        return new String(bytePlainText);
    }
```

<b></b>


Figure 2 shows the results after running the code.

![No alt text provided for this
image](../myMediaFolder/media/Capture%2067.PNG)

**Figure 2**

## 2. CBC mode

For CBC mode, I will use the same secret key to decrypt and encrypt.

The following method is used to encrypt data by using CBC mode. The method will return encrypted data as a list of bytes. The method required the secret key and the plain text.

```
    public static byte[] encryptText_CBC(String plainText,SecretKey secKey) throws Exception{
        Cipher aesCipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        aesCipher.init(Cipher.ENCRYPT_MODE, secKey);
        byte[] byteCipherText = aesCipher.doFinal(plainText.getBytes());
        return byteCipherText;
    }
```

<b></b>
<b></b>

The following method is used to decrypt data by using CBC mode. The method will return decrypt data as string. The method required the secret key and a list of bytes (encrypted text).

```
    public static String decryptText_CBC(byte[] byteCipherText, SecretKey secKey) throws Exception {
        IvParameterSpec iv = new IvParameterSpec(initVector.getBytes("UTF-8"));
        Cipher aesCipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        aesCipher.init(Cipher.DECRYPT_MODE, secKey, iv);
        byte[] bytePlainText = aesCipher.doFinal(byteCipherText);
        return Base64.getMimeEncoder().encodeToString(bytePlainText);
    }
```

<b></b>

Figure 3 shows the results after running the code by using two different modes.

![No alt text provided for this
image](../myMediaFolder/media/Capture%20688.PNG)

**Figure 3**
<b></b>