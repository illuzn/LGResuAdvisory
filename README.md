# LGES 5048 Inverter - LG Chem Battery Potential Vulnerability Advisory

## Precis
The LGES 5048 Inverter continues to broadcast its own Wifi SSID even when configured to join the customer's home wifi network. 

This is compounded by the fact that:

1. The installation manual for the LGES 5048 Inverter does not instruct the installer to change the Wifi password.
2. The installer password for the LGES 5048 Inverter cannot be changed. The installer password allows the user to change the regulatory environment of the Inverter potentially violating regulatory requirements.

## Detailed Description
### 1. LGES 5048
The LGES 5048 is a rebranded GoodWe Inverter. This investigation relates purely to the LG variant of this inverter but further investigation is recommended to investigate whether this vulnerability exists with the GoodWe variant or other GoodWe Inverters.

### 2. Solar-Wifi
By default, the LGES 5048 broadcasts its own Wifi SSID (**Internal SSID**) using `Solar-WifiXXXXXXXX` where XXXXXXXX is the last 8 digits of the serial number of the inverter. As set out in the installation manual, the password for the Internal SSID is `12345678`

The usual expected behavior would be that the inverter ceases to broadcast the Internal SSID once the customer's WiFi network is burned in. However, this is not the case, the Internal SSID continues to be broadcast even when connected to the customer's WiFi. N.B. It is not a solution to cease broadcasting the Internal SSID when connected to the customer's Wifi because WiFi jamming devices can be utilised to jam the WiFi connection between the inverter and the customer's WiFi network.

This is further compounded because the installation manual for the LGES 5048:

1. Does **_not_** mention that the Internal SSID will continue to be broadcast even when connected to the customer's Wifi.
2. Does **_not_** recommend changing the password for the Internal SSID.

<details>
  <summary>Extract from Pages 21 and 22 of LGES 5048 Installation Manual</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/57167030/175880362-c214569d-ef42-4b04-ac5e-4eff74b2d392.png">
  <img src="https://user-images.githubusercontent.com/57167030/175880983-69e38c41-15fa-416a-8cd7-a9c2f0cf461a.png">
</details>

The Authors installer (being electricians and not IT consultants) accordingly, did not change the password or raise the issue with the customer.

It is expected that many installs around Australia will thus be broadcasting the Internal SSID with the default password.

### LG PV Master
The security model of this inverter relies solely upon unauthorised users **_not_** being able to connect to the Inverter. As seen in section 2 above, it is expected that for a standard installation performed according to the installation manual the Internal SSID will be broadcast using the default (and very insecure) password.

It might be argued that there is a secondary level of protection via the installer password. However, this is illusory because:

1. The installer password is displayed in plain text in the installer manual.
2. The installation manual explicitly states that this password cannot be changed.

<details>
  <summary>Extract from of password and page from LG PV Master Installation Manual</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/57167030/175883689-4f3ce7d3-a0e5-4a35-88d8-9d8577c95a8d.png">
  <img src="https://user-images.githubusercontent.com/57167030/175883855-981270ac-d0e1-46bb-8473-5342e8980aca.png">
</details>

Once access as an installer is obtained (which for the vast majority of installations should be achieveable using publicly available information), a multitude of settings which should be secure can be changed unbeknownst to the customer.

<details>
  <summary>Some settings that really shouldn't be changed by the end user or that may breach technical requirements if changed</summary>
  <br>
1. Regulatory environment. The Author has not tested what the result would be if the regulatory environment is changed to one from another incompatible region.<br>
<img src="https://user-images.githubusercontent.com/57167030/175884384-17067360-74bd-4d1e-88e8-e6ef9d0a8e4c.png">
2. Battery Model. The Author has not tested what the result would be if a lower capacity battery model is selected. Presumably the BMS would protect against any overcharge/ overcurrent situations; however, a customer might get lower capacity than they have paid for if this was changed unknowingly.<br>
<img src="https://user-images.githubusercontent.com/57167030/175884649-27b80f62-2d00-4d4d-b8a8-a6796de02272.png">
3. Setting Battery Forced Charging. The Author would hope that this does not allow charging a battery at 100% state of charge - this has not been tested.<br>
<img src="https://user-images.githubusercontent.com/57167030/175885334-6b0f0d45-bc31-47bb-870c-a912f8e0a491.png">
4. Setting regulated parameters. The Author has not tested what the result would be if these parameters are changed; however, presumably they would cause this equipment to be in violation of technical regulations regarding power supply.<br>
<img src="https://user-images.githubusercontent.com/57167030/175885759-3d39dff1-5ee2-429e-a19d-f91f878efac1.png">
</details>

## Mitigation
The Author recommends that all customers immediately change the password of their Internal SSID.

## Copyright/ Intellectual Property
The LG trademark is used purely with fair use to refer to their products. No association or relationship with LG is intended or implied through the use of this trademark.
All images used on this website are extracted from the manual for the LGES 5048 Inverter. These images are used under fair use to facilitate the discussion on this page.


## Thanks
I would like to thank Solar Quotes for their amazing website and freely available resources.
