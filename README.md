# SQL

### ‼️ Proceed with caution. You may finish cutovers early 🍺 You may have more free time 🏄‍
## 🤦‍Or you may delete all the phones! Please avoid career limiting moves, ask questions!


##### First, let's list all the table names:

```sh
admin: run sql select tabname from systables
```

##### You should recognize some of the more common ones (below with description)
| Table | Description |
| ------ | ------ |
| [numplan](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#numplan) | List of all directory numbers and patterns |
| [sipdevice](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#sipdevice) | Contains data for SIP Trunk implementation |
| [device](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#device) | Lists every device in system from the CallManager perspective |
| [enduser](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#enduser) | Lists the end users for the system |
| [devicepool](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#devicepool) | Common collections of device attributes |
| [callingsearchspace](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#callingsearchspace) | Devices call to a calling search space made up of route partitions|
| [routepartition](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#routepartition) | A list of partitions for numplan |
| [endusernumplanmap](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#endusernumplanmap) | Many to many relationship between EndUsers and DNs |
| [enduserdevicemap](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#enduserdevicemap) | Control association between users and devices (many to many) |
| [devicenumplanmap](https://d1nmyq4gcgsfi5.cloudfront.net/media/UCM-DD-11-0-1/datadictionary.11.0.1.html#devicenumplanmap) | Ordered association of NumPlan records with a device (line appearance)|


> Now lets try some simple queries using what we learned:
SELECT <column name> from <tablename> where <constraints>
UPDATE <tablename> set <column name> = “<value>” where <constraints>
DELETE from <tablename> where <constraints>
INSERT into <tablename> (<columns>) values (“<values>”)

### #1 

##### Find information about endusers

```sh
admin:run sql select * from enduser
(omitted)
```

This is a lab, otherwise that would be a **BAD** idea. Try returning the first 3 users

```sh
admin:run sql select first 3 * from enduser
pkid                                 assocpc firstname middlename lastname userid                                          manager department     telephonenumber tkuserlocale mailid                  status facsimiletelephonenumber mobile pager homephone title                building site fkdirectorypluginconfig              uniqueidentifier                 nickname deletedtimestamp passwordreverse                                                  fkmatrix_presence                    tkuserprofile fkcallingsearchspace_restrict allowcticontrolflag enablemobilevoice maxdeskpickupwaittime enablemobility remotedestinationlimit ocsprimaryuseraddress enableemcc fkucserviceprofile directoryuri islocaluser fkucuserprofile enablecalendarpresence enablecups primarynodeid keypadenteredalternateidentifier discoveryuseridentity displayname   enableusertohostconferencenow conferencenowaccesscode userrank
==================================== ======= ========= ========== ======== =============================================== ======= ============== =============== ============ ======================= ====== ======================== ====== ===== ========= ==================== ======== ==== ==================================== ================================ ======== ================ ================================================================ ==================================== ============= ============================= =================== ================= ===================== ============== ====================== ===================== ========== ================== ============ =========== =============== ====================== ========== ============= ================================ ===================== ============= ============================= ======================= ========
e1fe1a69-c740-49c5-81d7-853e0d66938a                              Token    Token_User_592c0a99-e4f2-4146-93de-37f7c5b1faf1                                        NULL                                 1                                                                                         NULL                                                                           NULL             69c4f936f9cdf45f6bbca2570c31215629bb5d6fb97493478b8ff3db6fffbc55 ad243d17-98b4-4118-8feb-5ff2e1b781ac 3             NULL                          t                   f                 10000                 t              4                                            f          NULL                            t           NULL            f                      f          NULL          NULL                                                                 f                                                     1
087cb605-b476-08c7-792c-d9045b02b316         Michael              Scott    mscott                                                                 +19197016700    NULL         mscott@car.pnslabs.com  1                                                                                         05914b08-fa56-96f7-29d6-6b8de90e0346 ffb21c8fbc11234398eaadc64f7f611d          NULL             0c3ed3e34361b5121b792f546c53d809d1564fc458c60a47d59556e269954944 ad243d17-98b4-4118-8feb-5ff2e1b781ac 1             NULL                          t                   f                 10000                 t              4                                            f          NULL                            t           NULL            t                      t          1100          19197016700                      mscott@pnslabs.com    Michael Scott t                             1234                    1
67ddd615-0840-f3bb-dcda-532446ca589f         Pam                  Beesly   pbeesly                                         mscott  Administrative +19197016701    NULL         pbeesly@car.pnslabs.com 1                                                      Office Administrator               05914b08-fa56-96f7-29d6-6b8de90e0346 a96558edb5003d4fb3c7f0bd448c99c2          NULL             0c3ed3e34361b5121b792f546c53d809d1564fc458c60a47d59556e269954944 ad243d17-98b4-4118-8feb-5ff2e1b781ac 1             NULL                          t                   f                 10000                 t              4                                            f          NULL                            t           NULL            t                      t          1100          19197016701                      pbeesly@pnslabs.com   Pam Beesly    f                             1234                    1
```


### 💁‍Return all details from the enduser whose number is 6700 
This is actually pretty useful since **CUCM can't search end users based on number!**

```sh
admin:run sql select * from enduser where telephonenumber = '6700'
pkid assocpc firstname middlename lastname userid manager department telephonenumber tkuserlocale mailid status facsimiletelephonenumber mobile pager homephone title building site fkdirectorypluginconfig uniqueidentifier nickname deletedtimestamp passwordreverse fkmatrix_presence tkuserprofile fkcallingsearchspace_restrict allowcticontrolflag enablemobilevoice maxdeskpickupwaittime enablemobility remotedestinationlimit ocsprimaryuseraddress enableemcc fkucserviceprofile directoryuri islocaluser fkucuserprofile enablecalendarpresence enablecups primarynodeid keypadenteredalternateidentifier discoveryuseridentity displayname enableusertohostconferencenow conferencenowaccesscode userrank
==== ======= ========= ========== ======== ====== ======= ========== =============== ============ ====== ====== ======================== ====== ===== ========= ===== ======== ==== ======================= ================ ======== ================ =============== ================= ============= ============================= =================== ================= ===================== ============== ====================== ===================== ========== ================== ============ =========== =============== ====================== ========== ============= ================================ ===================== =========== ============================= ======================= ========

```

That didn't return anything. Lets search numbers that end in 6700 instead

```sh
admin:run sql select * from enduser where telephonenumber like '%6700'
pkid                                 assocpc firstname middlename lastname userid manager department telephonenumber tkuserlocale mailid                 status facsimiletelephonenumber mobile pager homephone title building site fkdirectorypluginconfig              uniqueidentifier                 nickname deletedtimestamp passwordreverse                                                  fkmatrix_presence                    tkuserprofile fkcallingsearchspace_restrict allowcticontrolflag enablemobilevoice maxdeskpickupwaittime enablemobility remotedestinationlimit ocsprimaryuseraddress enableemcc fkucserviceprofile directoryuri islocaluser fkucuserprofile enablecalendarpresence enablecups primarynodeid keypadenteredalternateidentifier discoveryuseridentity displayname   enableusertohostconferencenow conferencenowaccesscode userrank
==================================== ======= ========= ========== ======== ====== ======= ========== =============== ============ ====================== ====== ======================== ====== ===== ========= ===== ======== ==== ==================================== ================================ ======== ================ ================================================================ ==================================== ============= ============================= =================== ================= ===================== ============== ====================== ===================== ========== ================== ============ =========== =============== ====================== ========== ============= ================================ ===================== ============= ============================= ======================= ========
087cb605-b476-08c7-792c-d9045b02b316         Michael              Scott    mscott                    +19197016700    NULL         mscott@car.pnslabs.com 1                                                                          05914b08-fa56-96f7-29d6-6b8de90e0346 ffb21c8fbc11234398eaadc64f7f611d          NULL             0c3ed3e34361b5121b792f546c53d809d1564fc458c60a47d59556e269954944 ad243d17-98b4-4118-8feb-5ff2e1b781ac 1             NULL                          t                   f                 10000                 t              4                                            f          NULL                            t           NULL            t                      t          1100          19197016700                      mscott@pnslabs.com    Michael Scott t                             1234                    1
```

> 👉 Notice the % sign. This is a wildcard you can put on the beginning or end of your query. 

### #2
##### Let's look at how end users and devices are associated
#
> 👉 Remember, end users and devices are associated in the **enduserdevicemap** table


```sh
admin:run sql select * from enduserdevicemap
pkid                                 fkenduser                            fkdevice                             defaultprofile description tkuserassociation
==================================== ==================================== ==================================== ============== =========== =================
a03a9710-9e91-4f9b-bfff-a3da2796646b a77cc950-c07f-d163-3a97-231258b05cb1 3e6b09d8-054f-f6db-a6f2-2dcb578ad7d4 f                          1
dd59ecda-1171-4f37-b083-3d66c7738602 791e69c3-0624-531f-18dd-d4533a673090 e3d27f60-a03a-6eda-b343-11b2005232db f                          1
1d53e339-8a69-4d7a-af03-1f57ce825200 087cb605-b476-08c7-792c-d9045b02b316 904977a3-6089-ac4b-c524-8d43a86fa1fc f                          1
3fb0fcbd-7496-4286-a428-e41f22421eb8 087cb605-b476-08c7-792c-d9045b02b316 68949547-fe58-cd55-a3c2-a6c5104b927f f                          1
b50e0e65-fe8f-414f-b863-7d163f68f5dd 087cb605-b476-08c7-792c-d9045b02b316 70cf0740-7a49-4329-a394-7077cfee4192 f                          1
7c089a7a-7e5a-4f9e-986c-6f9e310981a7 087cb605-b476-08c7-792c-d9045b02b316 79b28500-8af9-1cb5-4996-26053ca9ddbf f                          1
0afbd740-fb54-4530-8f95-a9d5e533e7d4 67ddd615-0840-f3bb-dcda-532446ca589f 5cdd0622-39a8-f9cd-51e5-828935e84e27 f                          1
a85db7e5-3970-434b-9bb2-7262572fcad1 67ddd615-0840-f3bb-dcda-532446ca589f 201c998c-faa1-4955-23d1-95450d10ecae f                          1
```
Notice the fkenduser and fkdevice. These refer to the pkid of the enduser or device


### 🤵 Find devices associated to Michael Scott (mscott)

First find the pkid of mscott:
```sh
admin:run sql select pkid from enduser where userid like 'mscott'
pkid
====================================
087cb605-b476-08c7-792c-d9045b02b316
```

Next find the device pkids of devices associated to mscott
```sh
admin:run sql select * from enduserdevicemap where fkenduser = '087cb605-b476-08c7-792c-d9045b02b316'
pkid                                 fkenduser                            fkdevice                             defaultprofile description tkuserassociation
==================================== ==================================== ==================================== ============== =========== =================
1d53e339-8a69-4d7a-af03-1f57ce825200 087cb605-b476-08c7-792c-d9045b02b316 904977a3-6089-ac4b-c524-8d43a86fa1fc f                          1
3fb0fcbd-7496-4286-a428-e41f22421eb8 087cb605-b476-08c7-792c-d9045b02b316 68949547-fe58-cd55-a3c2-a6c5104b927f f                          1
b50e0e65-fe8f-414f-b863-7d163f68f5dd 087cb605-b476-08c7-792c-d9045b02b316 70cf0740-7a49-4329-a394-7077cfee4192 f                          1
7c089a7a-7e5a-4f9e-986c-6f9e310981a7 087cb605-b476-08c7-792c-d9045b02b316 79b28500-8af9-1cb5-4996-26053ca9ddbf f                          1
60f79ee6-f27d-487a-8609-73bc26f0d9b4 087cb605-b476-08c7-792c-d9045b02b316 a6d8ad5a-965d-7b87-631f-fdaf82cd428d f                          1
```

Now find the device(s) from the pkid(s)
```sh
admin:run sql select name from device where pkid = '904977a3-6089-ac4b-c524-8d43a86fa1fc'
name
===============
SEP84802D7747FB
```

>You can print all user device association by using multiple selectors

```sh
admin:run sql select enduser.userid, device.name from enduser, device, enduserdevicemap where enduserdevicemap.fkenduser = enduser.pkid and enduserdevicemap.fkdevice = device.pkid
userid      name
=========== ===============
jhalpert    SEP3C08F67A960A
pbeesly     SEPE4C7226B302B
pbeesly     SEP1CDEA78380DE
pbeesly     csfpbeesly
pbeesly     pbeesly_ipc
jhalpert    SEP0C2724311DD3
levensailor SEP005060051174
jhalpert    jhalpert_ipc
jhalpert    SEP2834A282A26C
pbeesly     SEP2834A282A26C
jhalpert    csfjhalpert
mscott      TCTMSCOTT
mscott      csfmscott
mscott      mscott_ipc
mscott      SEP84802D7747FB
mscott      SEPF8A5C59E0F1C
dschrute    SEP203A07822B2E
```

For reference later, lets print the entire device table:

```sh
admin:run sql select first 2 * from device where name like 'SEP%'
pkid                                 name            description     tkmodel tkdeviceprotocol tkprotocolside specialloadinformation fkdevicepool                         fkphonetemplate                      fkcallingsearchspace                 ctiid tkclass fkprocessnode defaultdtmfcapability fklocation                           tkproduct dialplanwizardgenid deviceleveltraceflag fkenduser                            allowhotelingflag tkdeviceprofile ikdevice_defaultprofile fkmediaresourcelist userholdmohaudiosourceid networkholdmohaudiosourceid unit subunit tkcountry tkuserlocale tkproduct_base fkcallingsearchspace_aar fkaarneighborhood fksoftkeytemplate retryvideocallasaudio routelistenabled fkcallmanagergroup tkstatus_mlppindicationstatus tkpreemption tkstatus_builtinbridge mtprequired tkqsig tkpacketcapturemode packetcaptureduration authenticationstring tkcertificatestatus upgradefinishtime fkmlppdomain transmitutf8 ignorepi tknetworklocation v150modemrelaycapable tkcertificateoperation fksecurityprofile                    fkdialrules fkcallingsearchspace_reroute         fkcallingsearchspace_refer unattended_port tkdtmfsignaling requiredtmfreception publickey fksipprofile                         rfc2833disabled allowcticontrolflag datetimeinserted sshpassword sshuserid fkcallingsearchspace_restrict        fkmatrix_presence                    fkcommonphoneconfig                  tkkeyauthority tksipcodec_mtppreferredorigcodec md5hash srtpallowed isstandard resettoggle tkreset versionstamp                                    fkcommondeviceconfig                 huntlistforvm remotedevice tkstatus_devicemobilitymode dndtimeout tkdndoption tkringsetting_dnd isdualmode fkcallingsearchspace_cgpntransform fkenduser_mobility tkoutboundcallrollover tkphonepersonalization tkstatus_joinacrosslines tkbarge tkstatus_usetrustedrelaypoint istrustedrelaypoint srtpfallbackallowed ispaienabled isrpidenabled tksipprivacy tksipassertedtype fkcallingsearchspace_cdpntransform usedevicepoolcdpntransformcss nationalprefix internationalprefix unknownprefix subscriberprefix usedevicepoolcgpntransformcss ikdevice_primaryphone tkstatus_audiblealertingidle tkstatus_audiblealertingbusy isactive tkphoneservicedisplay isprotected fkmobilesmartclientprofile tkstatus_alwaysuseprimeline tkstatus_alwaysuseprimelineforvm callednationalprefix calledinternationalprefix calledunknownprefix calledsubscriberprefix callednationalstripdigits calledinternationalstripdigits calledunknownstripdigits calledsubscriberstripdigits fkcallingsearchspace_callednational fkcallingsearchspace_calledintl fkcallingsearchspace_calledunknown fkcallingsearchspace_calledsubscriber hotlinedevice fkgeolocation fkgeolocationfilter_lp sendgeolocation nationalstripdigits internationalstripdigits unknownstripdigits subscriberstripdigits fkcallingsearchspace_cgpnnational fkcallingsearchspace_cgpnintl fkcallingsearchspace_cgpnunknown fkcallingsearchspace_cgpnsubscriber usedevicepoolcalledcssnatl usedevicepoolcalledcssintl usedevicepoolcalledcssunkn usedevicepoolcalledcsssubs pstnaccess fkvipre164transformation usedevicepoolcgpntransformcssnatl usedevicepoolcgpntransformcssintl usedevicepoolcgpntransformcssunkn usedevicepoolcgpntransformcsssubs fkfeaturecontrolpolicy runonallnodes enableixchannel tkdevicetrustmode usedevicepoolrdntransformcss fkcallingsearchspace_rdntransform enablebfcp requirecerlocation usedevicepoolcgpningressdn fkcallingsearchspace_cgpningressdn earlyoffersupportforvoicecall enablegatewayrecordingqsig calreference tkcalmode ndescription    msisdn fkwirelesslanprofilegroup enablecallroutingtordwhennoneisactive fkwifihotspotprofile allowcfbcontrolofcallsecurityicon fkelingroup ecpublickeycurve lscvaliduntil lscissuername lscissuervaliduntil
==================================== =============== =============== ======= ================ ============== ====================== ==================================== ==================================== ==================================== ===== ======= ============= ===================== ==================================== ========= =================== ==================== ==================================== ================= =============== ======================= =================== ======================== =========================== ==== ======= ========= ============ ============== ======================== ================= ================= ===================== ================ ================== ============================= ============ ====================== =========== ====== =================== ===================== ==================== =================== ================= ============ ============ ======== ================= ===================== ====================== ==================================== =========== ==================================== ========================== =============== =============== ==================== ========= ==================================== =============== =================== ================ =========== ========= ==================================== ==================================== ==================================== ============== ================================ ======= =========== ========== =========== ======= =============================================== ==================================== ============= ============ =========================== ========== =========== ================= ========== ================================== ================== ====================== ====================== ======================== ======= ============================= =================== =================== ============ ============= ============ ================= ================================== ============================= ============== =================== ============= ================ ============================= ===================== ============================ ============================ ======== ===================== =========== ========================== =========================== ================================ ==================== ========================= =================== ====================== ========================= ============================== ======================== =========================== =================================== =============================== ================================== ===================================== ============= ============= ====================== =============== =================== ======================== ================== ===================== ================================= ============================= ================================ =================================== ========================== ========================== ========================== ========================== ========== ======================== ================================= ================================= ================================= ================================= ====================== ============= =============== ================= ============================ ================================= ========== ================== ========================== ================================== ============================= ========================== ============ ========= =============== ====== ========================= ===================================== ==================== ================================= =========== ================ ============= ============= ===================
6a0ac8cf-d5d5-40ae-2d02-60b12c4046ee SEP0004F2E1413C SEP0004F2E1413C 431     0                1                                     b514d006-df40-ce53-b218-5fe09526d327 4f97c458-5036-4646-8dc4-65c842719078 1bf0ef13-7836-3b62-12f8-48fe2a168bee 33    1       NULL          0                     29c5c1c4-8871-4d1e-8394-0b9181e8c54d 330       NULL                f                    NULL                                 f                 0               NULL                    NULL                NULL                     NULL                        0    0       NULL      NULL         NULL           NULL                     NULL              NULL              t                     f                NULL               2                             2            2                      f           4      0                   0                                          1                                     NULL         f            f        2                 f                     1                      4cbf460c-ca43-4bbf-a936-8b3da7905cf3 NULL        NULL                                 NULL                       f               1               f                    NULL      NULL                                 f               t                   NULL                                   NULL                                 ad243d17-98b4-4118-8feb-5ff2e1b781ac ac243d17-98b4-4118-8feb-5ff2e1b781ac 0              1                                        f           f          t           2       1484079550-c52c3922-622c-4d38-99a0-be24c6df4a9d NULL                                 f             f            2                           0          0           NULL              f          NULL                               NULL               0                      3                      0                        0       2                             f                   f                   t            t             0            0                 NULL                               t                             Default        Default             Default       Default          t                             NULL                  2                            2                            t        3                     f           NULL                       2                           2                                Default              Default                   Default             Default                NULL                      NULL                           NULL                     NULL                        NULL                                NULL                            NULL                               NULL                                  f             NULL          NULL                   f               NULL                NULL                     NULL               NULL                  NULL                              NULL                          NULL                             NULL                                t                          t                          t                          t                          f          NULL                     t                                 t                                 t                                 t                                 NULL                   f             f               0                 t                            NULL                              f          f                  t                          NULL                               f                             f                          -1           NULL      SEP0004F2E1413C NULL   NULL                      f                                     NULL                 f                                 NULL        NULL             0             NULL          0
3e6b09d8-054f-f6db-a6f2-2dcb578ad7d4 SEP005060051174 Jeff's EX60     604     11               1                                     b514d006-df40-ce53-b218-5fe09526d327 524fc184-650e-4210-bb0a-10671d0482fd ea7f8e39-dc30-ab83-7397-c64bf2d84040 6749  1       NULL          0                     29c5c1c4-8871-4d1e-8394-0b9181e8c54d 491       NULL                f                    a77cc950-c07f-d163-3a97-231258b05cb1 f                 0               NULL                    NULL                NULL                     NULL                        0    0       NULL      NULL         NULL           NULL                     NULL              NULL              t                     f                NULL               0                             0            0                      f           4      0                   0                                          1                                     NULL         f            f        2                 f                     1                      514f85f5-456c-4ef9-8666-042d804a435c NULL        ea7f8e39-dc30-ab83-7397-c64bf2d84040 NULL                       f               1               f                    NULL      c89435ad-9385-3b3f-c3c2-b2a4c26ab267 f               t                   NULL                                   ea7f8e39-dc30-ab83-7397-c64bf2d84040 ad243d17-98b4-4118-8feb-5ff2e1b781ac ac243d17-98b4-4118-8feb-5ff2e1b781ac 0              1                                        f           f          f           2       1536962113-3c94d30b-3d15-495a-afe2-21f001a90ae1 a89a5d8d-6885-4029-a8bb-25dcd9354f38 f             f            2                           0          0           NULL              f          NULL                               NULL               0                      3                      0                        0       2                             f                   f                   t            t             0            0                 NULL                               t                             Default        Default             Default       Default          t                             NULL                  2                            2                            t        3                     f           NULL                       2                           2                                Default              Default                   Default             Default                NULL                      NULL                           NULL                     NULL                        NULL                                NULL                            NULL                               NULL                                  f             NULL          NULL                   f               NULL                NULL                     NULL               NULL                  NULL                              NULL                          NULL                             NULL                                t                          t                          t                          t                          f          NULL                     t                                 t                                 t                                 t                                 NULL                   f             f               0                 t                            NULL                              f          f                  t                          NULL                               f                             f                          -1           NULL      Jeff's EX60     NULL   NULL                      f                                     NULL                 f                                 NULL        NULL             0             NULL          0
```


### #3
##### Now lets look at how devices and directory numbers are associated
#
> 👉 Remember, devices and numbers are associated in the **devicenumplanmap** table
```sh
admin:run sql select * from devicenumplanmap
pkid                                 fkdevice                             numplanindex label                         fknumplan                            display                tkringsetting ctiid e164mask     dialplanwizardgenid tkmwlpolicy tkringsetting_consecutive maxnumcalls busytrigger callinfodisplaymask labelascii displayascii     tkringsetting_activepickupalert tkringsetting_idlepickupalert tkpartitionusage speeddial fkrecordingprofile fkcallingsearchspace_monitoring tkstatus_audiblemwi logmissedcalls tkpreferredmediasource
==================================== ==================================== ============ ============================= ==================================== ====================== ============= ===== ============ =================== =========== ========================= =========== =========== =================== ========== ================ =============================== ============================= ================ ========= ================== =============================== =================== ============== ======================
042d701c-cf63-44e5-a8d1-7959f8061041 2fc20049-3ffc-4419-a422-b317d30f67ab 1            #UserID# - #PrimaryExtension# NULL                                 #FirstName# #LastName# 4             1     NULL         NULL                0           0                         4           2           9                                               0                               0                             99               NULL      NULL               NULL                            2                   t              1
410d9458-c0c1-4ca2-a88a-4c4f29bf1988 815fa9a8-64b0-4191-a926-819a26cb1424 1            #UserID# - #PrimaryExtension# NULL                                 #FirstName# #LastName# 4             2                  NULL                0           0                         4           2           9                                               0                               0                             99               NULL      NULL               NULL                            2                   t              1
13034764-b2a3-6bc9-2123-e02b34c2a141 98ca9843-1911-14b8-8ce4-0f847796dfda 0                                          a4a7e445-5f0d-bbdc-6318-9611ac1e5d22                        4             3     NULL         NULL                0           0                         2           1           9                                               NULL                            NULL                          99               NULL      NULL               NULL                            2                   t              1
4dcc2837-5a31-f866-8bb2-21ffb63d415d 98ca9843-1911-14b8-8ce4-0f847796dfda 0                                          0ee9afeb-3e2a-e02a-a27c-24d190f719b2                        4             4     NULL         NULL                0           0                         2           1           9                                               NULL                            NULL                          99               NULL      NULL               NULL                            2                   t              1
7b016097-3ccf-6428-1d5b-516ab0bda234 98ca9843-1911-14b8-8ce4-0f847796dfda 0                                          6ac6eb49-7c97-68db-496e-b015b58b8959                        4             5     NULL         NULL                0           0                         2           1           9                                               NULL                            NULL                          99               NULL      NULL               NULL                            2                   t              1
722d5d64-e0fd-372d-e1b8-5873153769e2 70cf0740-7a49-4329-a394-7077cfee4192 1                                          d48f9648-0bdf-de66-9967-c896e90bf98b Michael Scott          4             6     +19197016700 NULL                0           0                         6           2           9                              Michael Scott    NULL                            NULL                          99               NULL      NULL               NULL                            2                   t              1
1baeabe1-8424-e521-76f6-b7fa6111883f 79b28500-8af9-1cb5-4996-26053ca9ddbf 1            6700                          b47dc671-d731-307e-e45c-0bcab6180c92 Michael Scott          0             7     +19197016700 NULL                0           0                         4           2           9                              Michael Scott    0                               0                             99               NULL      NULL               NULL                            2                   t              1
c422b191-d58b-0944-3096-b7779148c06e f7ac4cf9-f398-0fd2-462c-06e96bcc22fa 0                                          abb88c69-f309-73b5-130f-393f9265b6dd                        4             8     NULL         NULL                0           0                         2           1           9                                               NULL                            NULL                          99               NULL      NULL               NULL                            2                   t              1
d9ce99a2-c7f3-67f9-f152-6ff672558321 9feaf15d-822a-0d79-6c72-496706d8f962 1                                          1c077312-6841-fe4b-6040-954e59e18b48                        4             9     NULL         NULL                0           0                         10000       10000       9                                               NULL                            NULL                          99               NULL      NULL               NULL                            2                   t              1
890295b2-f275-3bef-ac33-e3633e41f82f 325009ab-4f56-995f-eb43-6042474ced34 1            6701                          480469e7-af50-c184-7932-90a1bcb9c7c7 Pam Beesly             0             10    +19197016701 NULL                0           0                         4           2           9                              Pam Beesly       0                               0                             99               NULL      NULL               NULL                            2                   t              1
f5967f5b-4fe1-be02-ac5f-1ff89ae9f8cc 1c230472-17eb-829e-c84b-4a145b4965b0 0                                          5a3da04e-521e-23d5-627b-6b38bb702608                        4             11    NULL         NULL                0           0                         2           1           9                                               NULL                            NULL                          99               NULL      NULL               NULL                            2                   t              1
ea7b2d79-6623-000a-9500-ae69fe7e5abb 46d5a84e-a7a4-d890-d5c4-3eaaaea76276 1            6702                          9e49b8ac-2087-e56c-de8b-4ea758e64623 Jim Halpert            0             12    +19197016702 NULL                0           0                         4           2           9                              Jim Halpert      0                               0                             99               NULL      NULL               NULL                            2                   t              1
```

Okay it looks like we have the bottom half of the directory number page in Call Manager

##### Let's look at directory numbers from the numplan table now:

```sh
admin:run sql select first 3 * from numplan where tkpatternusage = 2
pkid                                 fkroutepartition                     dnorpattern   tkpatternusage cfbdestination cfnadestination fkroutefilter tknetworklocation fkdigitdiscardinstruction prefixdigitsout blockenable tkmixer calledpartytransformationmask fkcallingsearchspace_sharedlineappear fkdialplan fkcallingsearchspace_translation callingpartytransformationmask patternurgency tkstatus_usefullyqualcallingpartynum fkcallingsearchspace_cfb             fkcallingsearchspace_cfna            dialplanwizardgenid userholdmohaudiosourceid networkholdmohaudiosourceid callforwardexpansionmask tkautoanswer personalroutingenabled devicefailuredn fkcallingsearchspace_devicefailure   callingpartyprefixdigits fkcallingsearchspace_mwi fkvoicemessagingprofile              cfbvoicemailenabled cfnavoicemailenabled cfdfvoicemailenabled fkaarneighborhood withtag withvalueclause description                   cfnaduration tkpatternprecedence cfaptvoicemailenabled cfaptdestination tkreleasecausevalue fkcallingsearchspace_cfapt tkpresentationbit_connectedline tkpresentationbit_callingname tkpresentationbit_connectedname tkpresentationbit_callingline supportoverlapsending cfaptduration iscallable fkcallmanager alertingname  authorizationcoderequired authorizationlevelrequired cfbintdestination cfbintvoicemailenabled cfnaintdestination cfnaintvoicemailenabled clientcoderequired cssforcfa fkcallingsearchspace_cfbint          fkcallingsearchspace_pff             fkcallingsearchspace_pffint          pff_cfb pff_cfna pffdestination pffintdestination pffintvoicemailenabled pffvoicemailenabled fkcallingsearchspace_reroute fkmatrix_presence                    fkcallingsearchspace_cfnaint         ismessagewaitingon outsidedialtone deviceoverride allowcticontrolflag alertingnameascii resettoggle tkreset aardestinationmask aarkeepcallhistory aarvoicemailenabled cfhrdn cfhrintdn cfhrintvmenabled cfhrvmenabled cfurdestination cfurintdestination cfurintvoicemailenabled cfurvoicemailenabled fkcallingsearchspace_cfhr fkcallingsearchspace_cfhrint fkcallingsearchspace_cfur            fkcallingsearchspace_cfurint         fkcallingsearchspace_revert hrduration hrinterval iknumplan_parkcode revertdestination cfhrduration tkdevicesecuritymode_minimumallowed tkcfacssactivationpolicy fkresourceprioritynamespace tknumberingplan_called tkpriofnumber_called tkpriofnumber_calling tknumberingplan_calling fkdevice_intercomdefault dnorpatternipv6 tkstatus_partyentrancetone parkmonforwardnoretrievedn parkmonforwardnoretrieveintdn parkmonforwardnoretrieveintvmenabled parkmonforwardnoretrievevmenabled fkcallingsearchspace_pkmonfwdnoret fkcallingsearchspace_pkmonfwdnoretint parkmonreversiontimer tkpatternrouteclass routenexthopbycgpn routeonuserpart usecallercss fkexternalcallcontrolprofile displayconnectedpartynumber rejectanonymouscall useoriginatorcss mlpppreemptiondisabled calreference tkcalmode dontwaitforidtatsubsequenthops nfkccaprofile_id isemergencyservicenumber
==================================== ==================================== ============= ============== ============== =============== ============= ================= ========================= =============== =========== ======= ============================= ===================================== ========== ================================ ============================== ============== ==================================== ==================================== ==================================== =================== ======================== =========================== ======================== ============ ====================== =============== ==================================== ======================== ======================== ==================================== =================== ==================== ==================== ================= ======= =============== ============================= ============ =================== ===================== ================ =================== ========================== =============================== ============================= =============================== ============================= ===================== ============= ========== ============= ============= ========================= ========================== ================= ====================== ================== ======================= ================== ========= ==================================== ==================================== ==================================== ======= ======== ============== ================= ====================== =================== ============================ ==================================== ==================================== ================== =============== ============== =================== ================= =========== ======= ================== ================== =================== ====== ========= ================ ============= =============== ================== ======================= ==================== ========================= ============================ ==================================== ==================================== =========================== ========== ========== ================== ================= ============ =================================== ======================== =========================== ====================== ==================== ===================== ======================= ======================== =============== ========================== ========================== ============================= ==================================== ================================= ================================== ===================================== ===================== =================== ================== =============== ============ ============================ =========================== =================== ================ ====================== ============ ========= ============================== ================ ========================
b47dc671-d731-307e-e45c-0bcab6180c92 64f031b8-b06a-bb39-cf16-91d86c500a65 \+19197016700 2                                             NULL          0                 NULL                      NULL            f           NULL    NULL                          NULL                                  NULL       NULL                             NULL                           t              2                                    cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                NULL                     NULL                        NULL                     0            f                                      cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                     NULL                     16c584ea-6a81-4138-9ea1-af452de8f75a t                   t                    t                    NULL                                      Michael Scott - \+19197016700 NULL         5                   f                                      0                   NULL                       0                               0                             0                               0                             f                     NULL          t          NULL          Michael Scott f                         0                                            t                                         t                       f                  NULL      cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 f       f                                         t                      t                   NULL                         ad243d17-98b4-4118-8feb-5ff2e1b781ac cee27a61-ad4f-3b29-a78f-aeb539334117 f                  f               f              t                   Michael Scott     f           1                          t                  f                   NULL   NULL      f                f                                                t                       t                    NULL                      NULL                         cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                        NULL       NULL       NULL               NULL              NULL         NULL                                0                        NULL                        0                      0                    0                     0                       NULL                                     2                                                                                   f                                    f                                 NULL                               NULL                                  NULL                  0                   f                  f               t            NULL                         f                           f                   f                f                      -1           NULL      f                              NULL             f
480469e7-af50-c184-7932-90a1bcb9c7c7 64f031b8-b06a-bb39-cf16-91d86c500a65 \+19197016701 2                                             NULL          0                 NULL                      NULL            f           NULL    NULL                          NULL                                  NULL       NULL                             NULL                           t              2                                    cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                NULL                     NULL                        NULL                     2            f                                      cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                     NULL                     16c584ea-6a81-4138-9ea1-af452de8f75a t                   t                    t                    NULL                                      Pam Beesly - \+19197016701    NULL         5                   f                                      0                   NULL                       0                               0                             0                               0                             f                     NULL          t          NULL          Pam Beesly    f                         0                                            t                                         t                       f                  NULL      cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 f       f                                         t                      t                   NULL                         ad243d17-98b4-4118-8feb-5ff2e1b781ac cee27a61-ad4f-3b29-a78f-aeb539334117 f                  f               f              t                   Pam Beesly        t           1                          t                  f                   NULL   NULL      f                f                                                t                       t                    NULL                      NULL                         cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                        NULL       NULL       NULL               NULL              NULL         NULL                                0                        NULL                        0                      0                    0                     0                       NULL                                     2                                                                                   f                                    f                                 NULL                               NULL                                  NULL                  0                   f                  f               t            NULL                         f                           f                   f                f                      -1           NULL      f                              NULL             f
9e49b8ac-2087-e56c-de8b-4ea758e64623 64f031b8-b06a-bb39-cf16-91d86c500a65 \+19197016702 2                                             NULL          0                 NULL                      NULL            f           NULL    NULL                          NULL                                  NULL       NULL                             NULL                           t              2                                    cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                NULL                     NULL                        NULL                     0            f                                      cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                     NULL                     16c584ea-6a81-4138-9ea1-af452de8f75a t                   t                    t                    NULL                                      Jim Halpert - \+19197016702   NULL         5                   f                                      0                   NULL                       0                               0                             0                               0                             f                     NULL          t          NULL          Jim Halpert   f                         0                                            t                                         t                       f                  NULL      cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 f       f                                         t                      t                   NULL                         ad243d17-98b4-4118-8feb-5ff2e1b781ac cee27a61-ad4f-3b29-a78f-aeb539334117 f                  f               f              t                   Jim Halpert       f           2                          t                  f                   NULL   NULL      f                f                                                t                       t                    NULL                      NULL                         cee27a61-ad4f-3b29-a78f-aeb539334117 cee27a61-ad4f-3b29-a78f-aeb539334117 NULL                        NULL       NULL       NULL               NULL              NULL         NULL                                0                        NULL                        0                      0                    0                     0                       NULL                                     2                                                                                   f                                    f                                 NULL                               NULL                                  NULL                  0                   f                  f               t            NULL                         f                           f                   f                f                      -1           NULL      f                              NULL             f
```
> 👉 Notice the tkpatternusage = 2, meaning any directory number.
For a full list, you can try **run sql select * from typepatternusage**

### 🏄‍ Time for some real world problems!

**Description** should adhere to a standard: **AlertingName** - **Directory Number**
```sh
admin:run sql update numplan set description = concat(concat(alertingname, '-'), dnorpattern) where tkpatternusage = 2 and description = “”
```
Some shared lines don't have the **Display** filled out. Use **Alerting Name** to fix. 

```sh
admin:run sql update devicenumplanmap dn set display = (select alertingname from numplan np where dn.fknumplan = np.pkid) where exists (select alertingname from numplan np where dn.fknumplan = np.pkid)
Rows: 78
```

Agents aren't sure which number to use when logging in to Finesse. Use Line Text Label to make this obvious

We can break this problem into smaller problems:
1. Find All IPCC Extensions (endusernumplanmap)
2. Find Devices these IPCC extensions are on
3. Update Line Text Label

IPCC extensions should have a tkdnusage = '2' according to the Data Dictionary:
```sh
admin:run sql select dnorpattern,pkid from numplan np where ((select tkdnusage from endusernumplanmap en where en.fknumplan = np.pkid) = '2')
dnorpattern pkid
=========== ====================================
87018701    9cc6b758-09e9-6581-f87e-a2915693a8ac
87018700    d48f9648-0bdf-de66-9967-c896e90bf98b
87018702    97d195a1-c85d-9b10-1bfc-efb5b2f0437e
```

To find the devices the IPCC Extensions are on, we'll do an **INNER JOIN**
Below is a simple join of device pkid and number:
```sh
admin:run sql select dn.fkdevice as device, np.dnorpattern as number from devicenumplanmap as dn inner join numplan as np on np.pkid = dn.fknumplan
device                               number
==================================== ====================================
0019eb57-2314-a7fd-df37-a99b4eaeac3e 5552005
073b61c6-fea1-2bf3-832a-04e731535a0f 88884444
0d6150db-d9e7-f778-a07f-89371afe2155 Line 1 Template - 8945 SIP PAPi Test
189ce396-3064-f6a3-b2bf-e5a15b8fb420 \+19197016702
1c230472-17eb-829e-c84b-4a145b4965b0 8889
1c230472-17eb-829e-c84b-4a145b4965b0 8885
1ee9795a-7661-2d58-605a-15bb56a4ca4a \+19197016701
201c998c-faa1-4955-23d1-95450d10ecae \+19197016701
21a50fc2-4926-d166-72fa-b6b0986c6892 87018701
325009ab-4f56-995f-eb43-6042474ced34 \+19197016701
35cdceb2-c175-2f9e-22a7-9c92c3abe8f7 5554444
3a518bf3-1b0d-2707-c098-f430177c8a34 \+19197016705
3dd7f83a-d9e6-fdc6-5826-98ec4c30d72c \+19197016702
omitted..
```

Now lets join together three tables to show the number usage:
```sh
admin:run sql select dn.fkdevice as device, en.tkdnusage as type, np.dnorpattern as number from devicenumplanmap as dn inner join numplan as np on np.pkid = dn.fknumplan inner join endusernumplanmap en on en.fknumplan = np.pkid
device                               type number
==================================== ==== =============
79b28500-8af9-1cb5-4996-26053ca9ddbf 1    \+19197016700
68949547-fe58-cd55-a3c2-a6c5104b927f 1    \+19197016700
904977a3-6089-ac4b-c524-8d43a86fa1fc 1    \+19197016700
70cf0740-7a49-4329-a394-7077cfee4192 2    87018700
79b28500-8af9-1cb5-4996-26053ca9ddbf 2    87018700
46d5a84e-a7a4-d890-d5c4-3eaaaea76276 2    87018702
46d5a84e-a7a4-d890-d5c4-3eaaaea76276 1    \+19197016702
3dd7f83a-d9e6-fdc6-5826-98ec4c30d72c 1    \+19197016702
61be946c-3092-ff9a-c065-fea49dc82e68 1    \+19197016702
189ce396-3064-f6a3-b2bf-e5a15b8fb420 1    \+19197016702
5cdd0622-39a8-f9cd-51e5-828935e84e27 1    \+19197016702
325009ab-4f56-995f-eb43-6042474ced34 1    \+19197016701
201c998c-faa1-4955-23d1-95450d10ecae 1    \+19197016701
1ee9795a-7661-2d58-605a-15bb56a4ca4a 1    \+19197016701
21a50fc2-4926-d166-72fa-b6b0986c6892 2    87018701
e3d27f60-a03a-6eda-b343-11b2005232db 1    \+19197016706
3e6b09d8-054f-f6db-a6f2-2dcb578ad7d4 1    8001
```

We can use a **WHERE** clause to filter this down to just dnusage of '2'
```sh
admin:run sql select dn.fkdevice as device, en.tkdnusage as type, np.dnorpattern as number from devicenumplanmap as dn inner join numplan as np on np.pkid = dn.fknumplan inner join endusernumplanmap en on en.fknumplan = np.pkid where en.tkdnusage = '2'
device                               type number
==================================== ==== ========
46d5a84e-a7a4-d890-d5c4-3eaaaea76276 2    87018702
21a50fc2-4926-d166-72fa-b6b0986c6892 2    87018701
70cf0740-7a49-4329-a394-7077cfee4192 2    87018700
79b28500-8af9-1cb5-4996-26053ca9ddbf 2    87018700
```
Okay it looks like our IPCC extensions fit a pattern, which makes our update a little easier:
```sh
admin:run sql update devicenumplanmap dn set label = concat('Agent - ',(select dnorpattern from numplan np where dn.fknumplan = np.pkid and dnorpattern like '8701870%')) where exists (select dnorpattern from numplan np where dn.fknumplan = np.pkid and dnorpattern like '8701870%')
Rows: 4
```

> 💡 If the IPCC extensions didn't follow a pattern, how could this be accomplished?


Lets go ahead and ensure the max number of calls and busy triggers are set appropriately
```sh
admin:run sql update devicenumplanmap dn set maxnumcalls = '2' where exists (select dnorpattern from numplan np where dn.fknumplan = np.pkid and dnorpattern like '8701870%')
Rows: 4

run sql update devicenumplanmap dn set busytrigger = '1' where exists (select dnorpattern from numplan np where dn.fknumplan = np.pkid and dnorpattern like '8701870%')
Rows: 4
```

Now let's validate
```sh
admin:run sql select label, maxnumcalls, busytrigger from devicenumplanmap where label like 'Agent%'
label            maxnumcalls busytrigger
================ =========== ===========
Agent - 87018700 1           1
Agent - 87018700 1           1
Agent - 87018702 1           1
Agent - 87018701 1           1
```

### #4
Lets take a look at translations. These are in the **numplan** table with a patternusage of '3'

```sh
admin:run sql select dnorpattern, calledpartytransformationmask, description from numplan where tkpatternusage=3
dnorpattern           calledpartytransformationmask description
===================== ============================= ===========================
87016XXX              +19197016XXX                  Enterprise xlate
6XXX                  +19197016XXX                  4 Digit xlate
9.1[2-9]XX[2-9]XXXXXX                               11 Digit PSTN
9.[2-9]XX[2-9]XXXXXX                                10 Digit PSTN
9011.!#                                             International
9011.!                                              International with T302
\+19197016703         87018801                      Xlate DID to CCX Main Menu
4545                  14052223001                   Shortcut dial
                      52808                         Ringdown for elevator phone
```

It's annoying to me when I have to click inside a translation to find what its being translated to. Let's add a description to tell administrators where the pattern goes. 

We want to retain the original description, ie: _Shortcut dial - +12024082022_

```sh
admin:run sql update numplan set description = concat(description,' - ',calledpartytransformationmask) where tkpatternusage=3 and calledpartytransformationmask is not NULL
Routine (concat) can not be resolved.
```

Looks like theres an error in the **CONCAT** statement. This can only concatenate two items. We'll use a concat of a concat. 

```sh
admin:run sql update numplan set description = concat(concat(description,' - '),calledpartytransformationmask) where tkpatternusage=3 and calledpartytransformationmask is not NULL
Rows: 9
```

Lets validate now:

```sh
admin:run sql select dnorpattern, calledpartytransformationmask, description from numplan where tkpatternusage=3
dnorpattern           calledpartytransformationmask description
===================== ============================= =====================================
87016XXX              +19197016XXX                  Enterprise xlate - +19197016XXX
6XXX                  +19197016XXX                  4 Digit xlate - +19197016XXX
9.1[2-9]XX[2-9]XXXXXX                               11 Digit PSTN
9.[2-9]XX[2-9]XXXXXX                                10 Digit PSTN
9011.!#                                             International
9011.!                                              International with T302
\+19197016703         87018801                      Xlate DID to CCX Main Menu - 87018801
4545                  14052223001                   Shortcut dial - 14052223001
                      52808                         Ringdown for elevator phone - 52808
```

Awesome time saver! 🤘

### #5
Speed Dials have their own special little table: **speeddial**

```sh
admin:run sql select first 10 * from speeddial
pkid                                 fkdevice                             speeddialindex speeddialnumber label        labelascii fkpersonalphonebook
==================================== ==================================== ============== =============== ============ ========== ===================
c2effa1c-d7da-ad6d-ade5-c07ffc63cba1 49b3fc31-da51-22f5-27bc-815361adb5dd 5              1019997         Dial By Name            NULL
cc2202cf-ae04-20bb-27ca-941fe135866f a9c40f99-e3cf-457f-6bf6-cb1e03bc01f3 7              1019997         Dial By Name            NULL
9ff1a103-3023-c9fc-e1a8-1c1cba5e3beb 930b59f5-fad1-f7dc-7d04-b2bc99f9ddc9 8              1019997         Dial By Name            NULL
8e5268f2-5ea2-50e5-193b-cce93d496602 37379851-6260-c87e-54ca-ecc12e58d2d2 8              1019997         Dial By Name            NULL
8f87b639-756e-cdb1-821c-0287349081cc ee661fd8-e70b-4544-b67a-b0bae5bdd015 8              1019997         Dial By Name            NULL
77dd9c5e-6fd6-4631-f2e4-2e3ab7289b24 a18abd27-e17e-b693-6a6b-4890e5c0b8b5 8              1019997         Dial By Name            NULL
c155c30b-5c8c-e6ac-bc69-acbb857e83e1 2fb1576b-fe1c-9435-ae13-0b0e5f84af65 8              1019997         Dial By Name            NULL
051a8a84-4000-1919-5eda-1d8d2414f39c 7af99140-513b-8f94-f8c8-fb93e3792553 5              1019997         Dial By Name            NULL
b8681ef4-3c83-a7ca-2502-d9e1eae28ce1 55856c5f-f388-fa2a-5792-ab24a3f9378f 8              1019997         Dial By Name            NULL
433d70fe-ce72-06f4-7584-737be2e63744 dcf3effe-c72c-704e-66d0-2303a84bed50 8              1019997         Dial By Name            NULL
```

The problem with speeddials is the index is only relative to buttons assigned as speeddial in the phone template. Assuming you want a "Dial By Name" speed dial to be the last button on every phone, Attorney-PBT would need a speedial index be 5 whereas the Secretary-PBT would need a speeddial index of 8.

| Template | Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 | Button 7 | Button 8 | Button 9 | Button 10 |
| -------- | -------- | -------- | -------- | --------- | ------- | -------- | -------- | -------- | -------- | --------- |
| Attorney-PBT | DN | BLF | SD | SD | SURL | Mobility | Intercom | SD | SD | SD| 
| Secretary-PBT | DN | DN | SD | SD | SD | SD | SD | SD | SD | SD |


Let's find the the phones assigned to **Attorney-PBT** template with a Dial By Name speeddial thats NOT on the last button. 

First we need the pkid of the Attorney-PBT template from the **phonetemplate** table:

```sh
admin:run sql select * from phonetemplate where name like 'Attorney-PBT'
pkid                                 name         numofbuttons usermodifiable tkmodel tkdeviceprotocol privatetemplate versionstamp                                    resettoggle tkreset
==================================== ============ ============ ============== ======= ================ =============== =============================================== =========== =======
66827fa4-5dd5-7e53-4017-ba333ff1e2c7 Attorney-PBT 82           t              684     11               f               1511820183-84684afb-e15c-46ed-9499-5c7777699503 f           2
```

Okay looks like there's quite a few:

```sh
admin:run sql select * from speeddial where label like 'Dial By Name' and speeddialindex <> '5' and speeddial.fkdevice in (select pkid from device where device.fkphonetemplate like '66827fa4-5dd5-7e53-4017-ba333ff1e2c7')
pkid                                 fkdevice                             speeddialindex speeddialnumber label        labelascii fkpersonalphonebook
==================================== ==================================== ============== =============== ============ ========== ===================
5c62489c-952c-9aca-0be5-79e1a4489606 00cad4dd-af20-a074-c1c9-314bc9cf35b8 6              1019997         Dial By Name            NULL
3ba8dc30-16c8-2562-3cde-ea098006612e 01c34e08-03c5-d4f7-fca6-f75bdf1566d8 6              1019997         Dial By Name            NULL
c3088a0b-ef62-2a83-7bcf-cd7ae50034a6 025f335f-4efe-a80f-74bd-4994ccbb8d7c 6              1019997         Dial By Name            NULL
93bea55a-6627-cff2-7f35-5a0f52d604d9 02ab519c-09bc-a37a-d35e-89f5fafd39bd 4              1019997         Dial By Name            NULL
b5c930b4-ab1b-e105-3335-a482fa9ec8a3 02c21ecd-afdf-7007-ca79-f6ea2ec1b96d 6              1019997         Dial By Name            NULL
```
> 👉 Notice the <> which means "not equal to" in SQL Lingo

Let's fix by updating **speeddialindex** to 8 (the last button for this template)
Changing the index of a button item is a great use case for sql. A small thing that saves a ton of time. 

```sh
admin:run sql update speeddial set speeddialindex = '8' where label like 'Dial By Name' and speeddial.fkdevice in (select pkid from device where device.fkphonetemplate = '66827fa4-5dd5-7e53-4017-ba333ff1e2c7')
Rows: 5
```

Here are some other useful **SELECT** queries for speeddials and blfspeeddials
> 👉 Notice the **by** at the end where I specify how the table is sorted

##### Joined table of speed dials and devices:
```sh
admin:run sql select d.name, d.description, sd.speeddialindex, sd.label, sd.speeddialnumber from speeddial as sd inner join device as d on sd.fkdevice=d.pkid order by d.name,sd.speeddialindex
name            description                      speeddialindex label                 speeddialnumber
=============== ================================ ============== ===================== ===============
SEP2834A282A26C Pam Beesly - 6701 - 2834A282A26C 1              mscott@presidio.cloud 670235
SEP2834A282A26C Pam Beesly - 6701 - 2834A282A26C 2                                    670233
SEPF8A5C59E0F1C Michael Scott - +19197016700     1              Pam Beesly            8888
SEPF8A5C59E0F1C Michael Scott - +19197016700     3              Jim Halpert           8887
SEPF8A5C59E0F1C Michael Scott - +19197016700     4                                    670235
SEPF8A5C59E0F1C Michael Scott - +19197016700     5                                    670239
```

##### Joined table of blf speed dials and devices:
```sh
admin:run sql select d.name, d.description, blf.blfindex, blf.label, blf.blfdestination from blfspeeddial as blf inner join device as d on blf.fkdevice=d.pkid order by d.name, blf.blfindex
name            description    blfindex label         blfdestination
=============== ============== ======== ============= ==============
SEP203A07822B2E Dwight Schrute 1        Michael Scott 6700
```


> 💡 Add Webex PMR speeddials to phones automatically using userid from enduser table to form the URI

### #6

Lets look at call forward settings in the **callforwarddynamic** table

```sh
admin:run sql select first 3 * from callforwarddynamic
pkid                                 cfadestination fkcallingsearchspace_cfa             cfavoicemailenabled fkcallingsearchspace_scfa            fknumplan                            datetimestamp
==================================== ============== ==================================== =================== ==================================== ==================================== =============
c9c52d00-4671-4bed-8b00-b26768ad2198 NULL           NULL                                 f                   NULL                                 00892849-2e18-4265-8a78-a6bdccf77b6e 1434754889
1cc18466-b4e4-40f7-9ae9-990414a93c60                cee27a61-ad4f-3b29-a78f-aeb539334117 f                   cee27a61-ad4f-3b29-a78f-aeb539334117 b47dc671-d731-307e-e45c-0bcab6180c92 1522787200
f9d2d466-f53e-41fc-b0ac-c59adf7dd57a                cee27a61-ad4f-3b29-a78f-aeb539334117 f                   cee27a61-ad4f-3b29-a78f-aeb539334117 480469e7-af50-c184-7932-90a1bcb9c7c7 1494982728
```

Notice the **datetimestamp**. This is because this is a **dynamic** table, meaning CUCM tracks state changes across devices that may both have control over these settings, and will take the latest setting. 

To find out what numbers have a **cfadestination** (call forward all) set, we use **callforwarddynamic** along with **numplan**

```sh
admin:run sql select n.dnorpattern, cf.cfadestination, cf.cfavoicemailenabled from numplan n inner join callforwarddynamic as cf on cf.fknumplan = n.pkid where cf.cfadestination <> ""
dnorpattern cfadestination cfavoicemailenabled
=========== ============== ===================
9749361     2152284        f
9748603     9748605        f
9741304     5906298        f
9741303     5906297        f
9741305     5906303        f
1015786     45141          f
9742495     9741680        f
9741870     99194459704    f
```

Similarly we can list numbers that have **cfavoicemailenabled** (call forward all to voicemail), and may want to also include the profile

```sh
admin:run sql select n.dnorpattern, vm.name, cf.cfavoicemailenabled from numplan n inner join voicemessagingprofile as vm on n.fkvoicemessagingprofile=vm.pkid inner join callforwarddynamic as cf on cf.fknumplan = n.pkid where cf.cfavoicemailenabled = 't'
dnorpattern   name    cfavoicemailenabled
============= ======= ===================
\+19197016706 Default t
52808         Old-VMP t
```

### #7

Sometimes you need to add a **partition** to several **calling search spaces** 

Let's take a look at these two common tables:

```sh
admin:run sql select first 3 * from callingsearchspace
pkid                                 name             description dialplanwizardgenid clause                                                                                                                 resettoggle tkreset tkpartitionusage
==================================== ================ =========== =================== ====================================================================================================================== =========== ======= ================
1bf0ef13-7836-3b62-12f8-48fe2a168bee RTPInternational             NULL                E164-Onnet-PT:RTPIntra:Directory URI:URI:ESN:onNetRemote:UStoE164:USPSTNNational:PSTNInternational:B2B_URI:USEmergency f           2       99
b6c26218-5aab-3eef-4e76-7a5e1b5f4987 RTPNational                  NULL                Directory URI:B2B_URI:E164-Onnet-PT:URI:ESN:onNetRemote:RTPIntra:UStoE164:USPSTNNational:USEmergency                   f           2       99
aef655f3-9c7f-a1ac-85a7-456768a78f86 RTPInternal                  NULL                E164-Onnet-PT:Directory URI:URI:ESN:onNetRemote:RTPIntra:UStoE164:B2B_URI:USEmergency                                  f           2       99
```

```sh
admin:run sql select first 3 * from routepartition where tkpartitionusage = '99'
pkid                                 name                               description                 dialplanwizardgenid fktimeschedule tktimezone useoriginatingdevicetimezone resettoggle tkreset tkpartitionusage
==================================== ================================== =========================== =================== ============== ========== ============================ =========== ======= ================
12e86f44-6e66-86e3-5337-353baeedc18a RTPIntra                           RTPIntra                    NULL                NULL           22         t                            f           2       99
8dbda30e-f5b8-6c8f-9590-a79fc3edc80e UStoE164                           UStoE164                    NULL                NULL           22         t                            f           2       99
319a9f31-d2dc-8622-4f03-4d5ecf21f7a7 USPSTNNational                     USPSTNNational              NULL                NULL           22         t                            f           2       99
87d6c9f5-7c79-9270-a07f-5477517a97af PSTNInternational                  PSTNInternational           NULL                NULL           22         t                            f           2       99
```

> 👉 Notice the tkpartitionusage = 99, meaning general usage CSS.
For a full list, you can try **run sql select * from typepartitionusage**

To add a partition, we'll do an **INSERT**

```sh
admin:run sql insert into routepartition (name,description) values ('Dodgers','World Series Champs')
Rows: 1
```
Now lets add this partition at the end of all CSS's

run sql update callingsearchspace set clause=concat(concat(clause,':'),'Dodgers') where tkpartitionusage = '99' 
> ❌This should give a permission error because you aren't allowed to edit the clause column directly. For that we have to use AXL

### #8

Services are in two tables: **telecasterservice** (all services) and **telecastersubscribedservice** (all instances of user-defined services)
### 🎸<-- actually a Stratocaster, but close enough :)

It's common for services to be subscribed multiple times to the same phone. To fix, you'll first get the pkid of the service (below):

```sh
admin:run sql select first 10 * from telecasterservice
pkid                                 name                urltemplate                                                        description            nameascii           tkphoneservice vendor version enterprisesubscription enabled priority tkphoneservicecategory secureurltemplate
==================================== =================== ================================================================== ====================== =================== ============== ====== ======= ====================== ======= ======== ====================== =================
d0059763-cdcc-4be7-a2a8-bbd4aac73f63 Missed Calls        Application:Cisco/MissedCalls                                      Missed Calls           Missed Calls        1                             t                      t       1        0                      NULL
0061bdd2-26c0-46a4-98a3-48a6878edf53 Received Calls      Application:Cisco/ReceivedCalls                                    Received Calls         Received Calls      1                             t                      t       2        0                      NULL
a0eed443-c705-4232-86d4-957295dd339c Placed Calls        Application:Cisco/PlacedCalls                                      Placed Calls           Placed Calls        1                             t                      t       3        0                      NULL
27f92f3c-11ed-45f3-8400-fe06431c0bfc Intercom Calls      Application:Cisco/IntercomCalls                                    Intercom Calls         Intercom Calls      1                             f                      t       4        0                      NULL
4a9d384a-5beb-4449-b176-cea0e8c4307c Personal Directory  Application:Cisco/PersonalDirectory                                Personal Directory     Personal Directory  1                             t                      t       5        0                      NULL
7eca2cf1-0c8d-4df4-a807-124b18fe89a4 Corporate Directory Application:Cisco/CorporateDirectory                               Corporate Directory    Corporate Directory 1                             t                      t       6        0                      NULL
ca69f2e4-d088-47f8-acb2-ceea6722272e Voicemail           Application:Cisco/Voicemail                                        Voicemail              Voicemail           2                             t                      t       1        0                      NULL
4496cbda-1633-3c4c-44be-6e2b02d6d00d extensionmobility   http://142.100.64.14:6293/ipphone/jsp/sciphonexml/IPAgentLogin.jsp                                            0                             f                      t       50       0
94b15fd7-ec11-4b5e-fcfb-6773b16e62b8 PAPi                http://10.144.200.33/PAPi/PAPi.php?device=#DEVICENAME#&Select=BAT  PAPi Auto Registration                     0                             f                      t       50       0
8a93187f-1622-4260-8016-ceeb7b151166 Honeycomb           http://10.144.200.33/PAPi/PAPi.php?device=#DEVICENAME#&Select=SMS                                             0                             f                      t       50       0
```

Now lets look at the **telecastersubscribedservice** table

```sh
admin:run sql select first 10 * from telecastersubscribedservice
pkid                                 fkdevice                             serviceurl                                                         servicename       fktelecasterservice                  urlbuttonindex urllabel           urllabelascii servicenameascii secureserviceurl priority
==================================== ==================================== ================================================================== ================= ==================================== ============== ================== ============= ================ ================ ========
55a5c5b5-d300-e91d-3efe-7f1588ae220e a6d8ad5a-965d-7b87-631f-fdaf82cd428d http://142.100.64.14:6293/ipphone/jsp/sciphonexml/IPAgentLogin.jsp extensionmobility 4496cbda-1633-3c4c-44be-6e2b02d6d00d 1              Extension Mobility                                NULL             NULL
1d62dcea-8b91-bc59-4834-300ebade8e13 815fa9a8-64b0-4191-a926-819a26cb1424 http://10.144.200.33/PAPi/PAPi.php?device=#DEVICENAME#             PAPi              94b15fd7-ec11-4b5e-fcfb-6773b16e62b8 0                                                                NULL             NULL
82f3fbf3-aa98-9a0c-4b8e-4bd717351de3 5cdd0622-39a8-f9cd-51e5-828935e84e27 http://10.144.200.33/PAPi/PAPi.php?device=#DEVICENAME#&Select=SMS  Honeycomb         8a93187f-1622-4260-8016-ceeb7b151166 0              Honeycomb                                         NULL             NULL
82f3fbf3-aa98-9a0c-4b8e-4bd717351de3 5cdd0622-39a8-f9cd-51e5-828935e84e27 http://10.144.200.33/PAPi/PAPi.php?device=#DEVICENAME#&Select=SMS  Honeycomb         8a93187f-1622-4260-8016-ceeb7b151166 1              Honeycomb                                         NULL             NULL
82f3fbf3-aa98-9a0c-4b8e-4bd717351de3 5cdd0622-39a8-f9cd-51e5-828935e84e27 http://10.144.200.33/PAPi/PAPi.php?device=#DEVICENAME#&Select=SMS  Honeycomb         8a93187f-1622-4260-8016-ceeb7b151166 2              Honeycomb                                         NULL             NULL
82f3fbf3-aa98-9a0c-4b8e-4bd717351de3 5cdd0622-39a8-f9cd-51e5-828935e84e27 http://10.144.200.33/PAPi/PAPi.php?device=#DEVICENAME#&Select=SMS  Honeycomb         8a93187f-1622-4260-8016-ceeb7b151166 3              Honeycomb                                         NULL             NULL
```

The ***fktelecasterservice** is the **pkid** from before. Each duplicate subscription will increment the **urlbuttonindex**.

Let's delete the duplicates:

```sh
admin:run sql delete from telecastersubscribedservice where fktelecasterservice = '8a93187f-1622-4260-8016-ceeb7b151166' and urlbuttonindex <> '1'
Rows: 3
``` 

### #9

I always try to use Device Pools for as much as possible, setting only whats unique on each actual phone.
Say we are upgrading and centralizing our CUBES (dspfarms) and need to change 100 device pools to use a new MRGL

First lets check out the **devicepool** table

```sh
admin:run sql select first 1 * from devicepool
pkid                                 name    fkregion                             fkdatetimesetting                    fkcallmanagergroup                   fkcallingsearchspace_autoregistration fkmediaresourcelist                  tkcountry fksrst                               connectionmonitorduration resettoggle tkreset versionstamp                                    fkaarneighborhood fkcallingsearchspace_aar fkcallingsearchspace_mobility fkdevicemobilitygroup fklocation fkphysicallocation tkrevertpriority tkstatus_joinacrosslines tkbarge fkcallingsearchspace_cdpntransform nationalprefix internationalprefix unknownprefix subscriberprefix fkcallingsearchspace_cgpntransform callednationalprefix calledinternationalprefix calledunknownprefix calledsubscriberprefix callednationalstripdigits calledinternationalstripdigits calledunknownstripdigits calledsubscriberstripdigits fkcallingsearchspace_callednational fkcallingsearchspace_calledintl fkcallingsearchspace_calledunknown fkcallingsearchspace_calledsubscriber fkcallingsearchspace_adjunct fkgeolocation fkgeolocationfilter_lp nationalstripdigits internationalstripdigits unknownstripdigits subscriberstripdigits fkcallingsearchspace_cgpnnational fkcallingsearchspace_cgpnintl fkcallingsearchspace_cgpnunknown fkcallingsearchspace_cgpnsubscriber fkviprpublisheddidpatterngroup fkcallingsearchspace_cntdpntransform fkcallingsearchspace_rdntransform fkcallingsearchspace_cgpningressdn fkwirelesslanprofilegroup fkelingroup
==================================== ======= ==================================== ==================================== ==================================== ===================================== ==================================== ========= ==================================== ========================= =========== ======= =============================================== ================= ======================== ============================= ===================== ========== ================== ================ ======================== ======= ================================== ============== =================== ============= ================ ================================== ==================== ========================= =================== ====================== ========================= ============================== ======================== =========================== =================================== =============================== ================================== ===================================== ============================ ============= ====================== =================== ======================== ================== ===================== ================================= ============================= ================================ =================================== ============================== ==================================== ================================= ================================== ========================= ===========
1b1b9eb6-7803-11d3-bdf0-00108302ead1 Default 1b1b9eb1-7803-11d3-bdf0-00108302ead1 9ec4850a-7748-11d3-bdf0-00108302ead1 d13c4201-7802-11d3-bdf0-00108302ead1 NULL                                  b2c6a8fd-83f3-13c9-f103-15424960b514 NULL      cd241e11-4a58-4d3d-9661-f06c912a18a3 -1                        t           1       1485790853-d88d207c-08b4-4953-8b45-1936f37bc199 NULL              NULL                     NULL                          NULL                  NULL       NULL               0                2                        3       NULL                               Default        Default             Default       Default          NULL                               Default              Default                   Default             Default                NULL                      NULL                           NULL                     NULL                        NULL                                NULL                            NULL                               NULL                                  NULL                         NULL          NULL                   NULL                NULL                     NULL               NULL                  NULL                              NULL                          NULL                             NULL                                NULL                           NULL                                 NULL                              NULL                               NULL                      NULL
```

Mostly everything is a foreign key, so we'll need to **update** referencing the pkid of the **mediaresourcelist**

Lets check the **mediaresourcelist** table

```sh
admin:run sql select  * from mediaresourcelist
pkid                                 name          clause                             resettoggle tkreset
==================================== ============= ================================== =========== =======
1f207892-b00d-c0e3-cba2-b2f069205109 SW_MRGL       SW_MRG                             f           2
b2c6a8fd-83f3-13c9-f103-15424960b514 HW_SW_MS_MRGL HW_MRG:SW_MRG:MS_MRG               f           2
3d62fb55-1e3b-91ca-8d1d-c3cf043e77d3 MS_HW_SW_MRGL MS_MRG:HW_MRG:SW_MRG               f           2
c9493f9e-0272-2dc0-4ddf-17ff9deb1d67 WILDLY_MRGL   WILDLY-HW_MRG:MS_MRG:SW_MRG:HW_MRG f           2
```

Now lets set all **devicepools** to HW_SW_MS_MRGL (Hardware first, then Software, also Mediasense.. remember that last one?)

```sh
admin:run sql update devicepool set fkmediaresourcelist = 'b2c6a8fd-83f3-13c9-f103-15424960b514'
Rows: 100
```

Nice!

### #10

I remember once having to spend a couple hours setting lines to "flash only". Never Again!

Ring settings are found in **devicenumplanmap** as **tkringsettingconsecutive**
As you may have guessed, you can find all the types of rings in another table:

```sh
admin:run sql select * from typeringsetting
enum name               moniker                 islinecompatible
==== ================== ======================= ================
0    Use System Default RING_SETTING_DEFAULT    t
1    Disable            RING_SETTING_DISABLE    t
2    Flash Only         RING_SETTING_FLASH_ONLY t
3    Ring Once          RING_SETTING_RING_ONCE  t
4    Ring               RING_SETTING_RING       t
5    Beep Only          RING_SETTING_BEEP_ONLY  f
```

Assuming shared lines are on line 2, let's change these to Flash Only

```sh
admin:run sql update devicenumplanmap set tkringsetting_consecutive='2' where numplanindex = 1
Rows: 6
```
> 👉 Notice I said line 2, but the index is 1. Just assume everything starts at zero. 

### #11

You may have times where your buttons don't match your phone button template, and this is confusing because everyone's phone in the office should look the same, right? For these situations you can change the index based on other information. 

#### Update Speed Dial index based on phone button template

```sh
admin:run sql update speeddial sd set sd.speeddialindex = '4' where sd.label like 'WebEx' and exists (select * from device d where d.fkphonetemplate like '66827fa4-5dd5-7e53-4017-ba333ff1e2c7' and d.description like 'Robert Hainey - +13467831726' and d.pkid = sd.fkdevice)
```

#### update speed dial index based on label, device pool and phone button template

```sh
admin:run sql update speeddial set speeddialindex = ‘4’ where label like ‘WebEx’ AND speeddial.fkdevice in (select pkid from device where device.fkphonetemplate like '62da8d7d-a885-ea31-5735-f90d95e575f6' and device.fkdevicepool like ‘cec8559c-3d22-4086-a27f-8cdfca4807a3’)
```

### #12

We've all ran into a situation where a directory number changes and calls are still going to the old number because there were multiple translations piped into that number. Translations have a description field that could easily contain the destination. 

#### take called party xform number and add it to translation pattern description

```sh
admin:run sql select dnorpattern, calledpartytransformationmask, description from numplan where tkpatternusage=3 and calledpartytransformationmask is not NULL
```

### #13

Intercoms need an extra step to accomodate for users with multiple devices, since an intercom is a one-to-one feature. In cases where a user needs an intercom and they only have one device, you can make that device the default activated device to complete the setup. 

#### Set intercom’s default activated device to the one its associated to

```sh
admin:run sql select d.pkid as dev, n.pkid as num from device d join devicenumplanmap dnpm on d.pkid = dnpm.fkdevice join numplan n on n.pkid = dnpm.fknumplan where tkpatternusage = 13 and fkdevice_intercomdefault is NULL
```

```sh
admin:run sql update numplan set fkdevice_intercomdefault = 'devpkid from before' where pkid = 'num pkid from before'
```
> 👉 Remember tkpatternusage 13 is an intercom dn
