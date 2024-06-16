# 📱 Temp-SMS-Receive

A Python script to fetch temporary SMS numbers and display received messages.

[![wakatime](https://wakatime.com/badge/user/018e35c7-dffb-4eaa-b21c-9bb81183371b/project/946f7b58-72c0-4ed3-a83f-1dc1d76f842a.svg)](https://wakatime.com/badge/user/018e35c7-dffb-4eaa-b21c-9bb81183371b/project/946f7b58-72c0-4ed3-a83f-1dc1d76f842a)
[![CodeFactor](https://www.codefactor.io/repository/github/sl-sanda-ru/temp-sms-receive/badge)](https://www.codefactor.io/repository/github/sl-sanda-ru/temp-sms-receive)
![GitHub License](https://img.shields.io/github/license/Sl-Sanda-Ru/Temp-SMS-Receive?color=green)


## ✨ Features

- 🌍 Fetches temporary SMS numbers from various countries.
- 📩 Displays SMS messages received by the fetched numbers.
- 📋 Copies selected number to the clipboard.
- 🔄 Handles dependencies automatically.
- 🎨 Includes a colorful and interactive CLI.
- 🔄 Automatic Update (via GIT)

## 🛠️ Prerequisites

- 🐍 Python 3.x
- 📦 PIP (Python package installer)

## 📥 Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/Sl-Sanda-Ru/Temp-SMS-Receive.git
    cd Temp-SMS-Receive
    ```

2. Install dependencies:

    ```bash
    pip install -r requirements.txt
    ```

## 🚀 Usage

1. Run the script:

    ```bash
    python tempsms.py
    ```

2. Follow the on-screen instructions to select a country and fetch temporary SMS numbers.

3. Choose a number to see the received SMS messages.

## 🔗 API Source

The API is extracted from the [Temp Number APP](https://play.google.com/store/apps/details?id=com.tempnumber.Temp_Number.Temp_Number).

## 🛠️ Tools Used

- **jadx-gui**: Assisted in decompiling the Java source code to find the decrypt key.
- **Magisk**: Used for SSL bypass.
- **HttpCanary**: Used for intercepting network traffic and analyzing HTTP requests.

## 🔍 Decompiled Java Source Code

This Java source code, decompiled using **jadx-gui**, helped to find the Authorization key:

```java
public void displayKeyData(EncryptedKeyResponse encryptedKeyResponse, String str) {
    String str2;
    if (encryptedKeyResponse == null || (str2 = encryptedKeyResponse.api_key) == null || str2.isEmpty()) {
        return;
    }
    char[] charArray = new Decryption().decryption(encryptedKeyResponse.api_key, this.sharedpreferences.getString("keyId", "")).toCharArray();
    StringBuilder sb = new StringBuilder();
    for (int i = 0; 32; i++) {
        sb.append(charArray[i]);
    }
    this.freeNumbersPresenter.getFreeNumber(new NumbersRequest(this.CountryName, this.page, 10), "Bearer " + ((Object) sb));
}

public String decryption(String str, String str2) {
    byte[] decode;
    try {
        if (Build.VERSION.SDK_INT >= 26) {
            decode = Base64.getDecoder().decode(str);
        } else {
            decode = android.util.Base64.decode(str, 0);
        }
        byte[] bArr = new byte[16];
        int length = decode.length - 16;
        byte[] bArr2 = new byte[length];
        System.arraycopy(decode, 0, bArr, 0, 16);
        System.arraycopy(decode, 16, bArr2, 0, length);
        SecretKeySpec secretKeySpec = new SecretKeySpec(str2.getBytes(), "AES");
        IvParameterSpec ivParameterSpec = new IvParameterSpec(bArr);
        Cipher cipher = Cipher.getInstance("AES/CBC/NoPadding");
        cipher.init(2, secretKeySpec, ivParameterSpec);
        return new String(cipher.doFinal(bArr2));
    } catch (Exception e) {
        e.printStackTrace();
        return null;
    }
}
```
## 🌟 Stargazers

[![Stargazers repo roster for @Sl-Sanda-Ru/Temp-SMS-Receive](https://reporoster.com/stars/dark/Sl-Sanda-Ru/Temp-SMS-Receive)](https://github.com/Sl-Sanda-Ru/Temp-SMS-Receive/stargazers)
[![Forkers repo roster for @Sl-Sanda-Ru/Temp-SMS-Receive](https://reporoster.com/forks/dark/Sl-Sanda-Ru/Temp-SMS-Receive)](https://github.com/Sl-Sanda-Ru/Temp-SMS-Receive/network/members)

## 👤 Author

Sandaru Ashen

- [GitHub](https://github.com/Sl-Sanda-Ru)
- [Telegram](https://t.me/Sl_Sanda_Ru)

## 📜 License

This project is licensed under the GPT-3.0
