got the idea from
https://xdaforums.com/t/cgm-app-blacklists-the-majority-of-phones-and-android-versions.4569881/

Renate:
First impression: The whitelist gets downloaded from here: https://carelink.minimed.com/api/connect/v1/client/config/gm/android/whitegraylist
Code:
{
    "3.4.0": {
...
    },
    "3.4.1": {
...
    },
    "3.4.2": {
...
    },
    "3.4.3": {
        "MAX_PHONE_SCREEN_CONFIG": 7,
        "WHITELIST": {
            "SM-N970X": {
                "description": "Galaxy Note10",
                "supportedOS": ["10.0.0", "11.0.0", "12.0.0"]
            },
            "SM-N970N": {
                "description": "Galaxy Note10",
                "supportedOS": ["10.0.0", "11.0.0", "12.0.0"]
            },
            "SM-N970W": {
                "description": "Galaxy Note10",
                "supportedOS": ["10.0.0", "11.0.0", "12.0.0"]
            },
...
        },
        "GRAYLIST": {
            "SONY": [9, 10, 11],
            "XIAOMI": [9, 10, 11],
            "LGE": [9, 10],
            "SAMSUNG": [7, 8, 9, 10, 11, 12, 13],
            "HUAWEI": [9, 10],
            "GOOGLE": [10, 11, 12, 13]
        },
        "BLACKLIST": {}
    }
}
Silly way #1 to fix this: Change the URL to your own website with edited JSON. :p


APK from
https://apkpure.com/guardian-connect/com.medtronic.diabetes.guardianconnect

https://apkpure.com/guardian-connect/com.medtronic.diabetes.guardianconnect/download/3.5.0

I have searched for the whitegraylist text in the decompiled 3.5.0 apk (decompiled with APK Editor Studio v1.7.1 from https://qwertycube.com/apk-editor-studio/download/)

Do not forget to decompile the "smali" part too:
Settings->Options->Apktool->check Decompile source code (smali)
The edited file:
smali/com/medtronic/guardian/ui/activities/carelink/t.smali

line 166 commented out, line 167 edited to my whitelist json file:
    162:invoke-interface {p0}, Lc/d/e/l/d/c;->l0()Ljava/lang/String;
    163:
    164: move-result-object p0
    165:
    166: #invoke-virtual {v0, p0}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;
    167:
    168: const-string p0, "https://raw.githubusercontent.com/wishmastersystem/medtronic_carelink_whitelist/main/whitegraylist.json"
    169:
    170: invoke-virtual {v0, p0}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

Then File -> Save APK
Installed my modified APK and worked with my DOOGEE phone.


