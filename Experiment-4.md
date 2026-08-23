# Experiment No. 4: Analyze Email Headers and Detect Email Spoofing Using MHA

## Aim

To analyze an email header using Mail Header Analyzer (MHA) and detect possible email spoofing by examining email routing information and authentication results.

## Requirements

* Gmail / Outlook / Yahoo Mail
* Mail Header Analyzer (MHA)
* Web browser
* WHOIS / IP lookup tool
* Internet connection

## Procedure

### Step 1: Access the Email Header

**Gmail:**

1. Open the email.
2. Click the three-dot menu in the upper-right corner.
3. Select **Show original**.

**Outlook:**

1. Open the email.
2. Click **File**.
3. Select **Properties**.
4. Locate the **Internet headers** section.

**Yahoo:**

1. Open the email.
2. Click the three-dot menu.
3. Select **View raw message**.
<img width="1600" height="615" alt="image" src="https://github.com/user-attachments/assets/7a23e1e6-a6bd-44ab-a67e-4ffc004c9b10" />

### Step 2: Copy the Email Header

Copy the complete email header displayed by the email service.
<img width="1915" height="788" alt="image" src="https://github.com/user-attachments/assets/4af02c10-6f70-45ef-829d-4b26b572aee7" />

### Step 3: Analyze the Header Using MHA

1. Open Mail Header Analyzer.
2. Paste the copied email header into the analyzer.
3. Submit the header for analysis.
4. Examine the parsed header information.
5. Identify the `From`, `To`, `Return-Path`, `Received`, and `Message-ID` fields.
6. Check the SPF, DKIM, and DMARC authentication results.
<img width="1060" height="484" alt="image" src="https://github.com/user-attachments/assets/d6845ea9-c05d-43fa-b7c1-7b1772baf66c" />

### Step 4: Analyze the Received Fields

Examine the `Received` fields to determine:

* Sending server hostname
* Sending server IP address
* Receiving server
* Date and time of transmission
* Sequence of mail servers

The `Received` headers should be analyzed from the **bottom upward** to trace the email's path.
<img width="1600" height="406" alt="image" src="https://github.com/user-attachments/assets/f56e4544-90ce-4bd9-af26-723461a5722f" />

### Step 5: Check IP Addresses and Hostnames

Use an IP lookup or WHOIS tool to check the IP addresses found in the `Received` headers.

Verify whether:

* The IP belongs to the expected mail server.
* The hostname matches the IP address.
* The sending server appears legitimate.
* Any unexpected server or IP address is present.
<img width="1078" height="258" alt="image" src="https://github.com/user-attachments/assets/04cf541b-6d21-42b8-90be-cb901a007f7c" />

### Step 6: Check SPF, DKIM, and DMARC

Record the authentication results.

| Check | Result    | Observation                                |
| ----- | --------- | ------------------------------------------ |
| SPF   | PASS/FAIL | Check whether the sending IP is authorized |
| DKIM  | PASS/FAIL | Check whether the DKIM signature is valid  |
| DMARC | PASS/FAIL | Check domain authentication and alignment  |
<img width="1832" height="868" alt="image" src="https://github.com/user-attachments/assets/5576757a-24bc-49aa-aefa-528d7ff49b4e" />
<img width="1811" height="538" alt="image" src="https://github.com/user-attachments/assets/a5eaf636-d776-42f6-8be7-59c47f57db93" />
<img width="1600" height="734" alt="image" src="https://github.com/user-attachments/assets/6b03e975-38df-44b2-b2c0-eddb7eabd10d" />
<img width="1600" height="750" alt="image" src="https://github.com/user-attachments/assets/9467862c-26cf-4e78-96e1-da9a1d468ecd" />

### Step 7: Analyze Message-ID

Check the domain used in the `Message-ID` and compare it with the sender's domain.
<img width="1394" height="313" alt="image" src="https://github.com/user-attachments/assets/a14972a9-45d2-46e4-b7de-6a52641ece75" />

### Step 8: Identify Possible Spoofing Indicators

Check for:

* `From` and `Return-Path` domain mismatch
* Suspicious IP addresses
* Unexpected hostnames
* SPF failure
* DKIM failure
* DMARC failure
* Unusual timestamps
* Inconsistent mail-server routing
* Suspicious Message-ID domain
  <img width="1600" height="311" alt="image" src="https://github.com/user-attachments/assets/0272e652-bea6-43e1-b3d6-c244444f28f1" />


## Observation

The email header was successfully parsed using MHA. The sender information, mail-server path, IP address, Message-ID, and email authentication results were examined for inconsistencies.

## Result

The email header was successfully analyzed using Mail Header Analyzer, and possible email spoofing indicators were identified by examining the **Received, Return-Path, Message-ID, SPF, DKIM, and DMARC** fields.

## Conclusion

Email header analysis using MHA can be used to trace the email's delivery path and identify inconsistencies that may indicate email spoofing or phishing.
