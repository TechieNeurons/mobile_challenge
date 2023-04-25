1. DL and extract the archive
2. open the apk with jadx-gui (apt-get install jadx)
3. Go in the main activity com.example.apkrypt - MainActivity
4. 

```
if (MainActivity.md5(MainActivity.this.ed1.getText().toString()).equals("735c3628699822c4c1c09219f317a8e9")) {
Toast.makeText(MainActivity.this.getApplicationContext(), MainActivity.decrypt("k+RLD5J86JRYnluaZLF3Zs/yJrVdVfGo1CQy5k0+tCZDJZTozBWPn2lExQYDHH1l"), 1).show();
```

5. If we enter the md5 **"735c3628699822c4c1c09219f317a8e9"** in the text area (**ed1**) then we get a "toast" giving us the VIP token **"k+RLD5J86JRYnluaZLF3Zs/yJrVdVfGo1CQy5k0+tCZDJZTozBWPn2lExQYDHH1l"**
6. To decrypt the VIP token us the **decrypt** function

```
public static String decrypt(String str) throws Exception {
        Key generateKey = generateKey();
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(2, generateKey);
        return new String(cipher.doFinal(Base64.decode(str, 0)), "utf-8");
    }
```

7. The decrypt is a simple AES of the b64 decode of the token, the AES key is in the function **generateKey** 

```
    private static Key generateKey() throws Exception {
        return new SecretKeySpec("Dgu8Trf6Ge4Ki9Lb".getBytes(), "AES");
    }
```

8. The key is **"Dgu8Trf6Ge4Ki9Lb"** by default the IV will be only 0
9. We can put everything in cyberchef (key = "Dgu8Trf6Ge4Ki9Lb", IV = 0, ECB/NoPadding)
