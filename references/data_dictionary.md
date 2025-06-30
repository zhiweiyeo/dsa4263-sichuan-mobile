# Data Dictionary

### APP (Application usage record)

| Feature Name       | Description |
|--------------------|-------------|
| `phone_number_m`     | Subscriber's anonymized phone number (main unique identifier of user). |
| `app_usage_count`    | Number of unique apps used by the phone number over 8 months. |
| `flow_mean`         | Average data usage across all app interactions over 8 months for the phone number (in MB). |
| `flow_median`        | Median data usage across all app interactions over 8 months for the phone number (in MB). |
| `flow_min`           | Minimum data usage across all app interactions over 8 months for the phone number (in MB). |
| `flow_max`           | Maximum data usage across all app interactions over 8 months for the phone number (in MB). |
| `flow_var`           | Variance in data usage across all app interactions over 8 months for the phone number (in MB). |
| `flow_sum`           | Total data usage across all app interactions over 8 months for the phone number (in MB). |
| `flow_month`         | Average data usage per month for the phone number (flow_sum / months_count). |
| `months_count`       | Number of months the user was active (from August 2019 to March 2020). |

### SMS (Short Message Service)

| Feature Name             | Description |
|--------------------------|-------------|
| `sms_count`                | Total number of SMS records per phone number across 8 months (messages sent and received). |
| `sms_nunique_contact`      | Number of unique contacts the subscriber exchanged SMS with over 8 months. |
| `sms_date_nunique`         | Total number of unique dates an SMS was sent over 8 months. |
| `sms_hour_mode`            | Most frequent hour (mode) SMS messages were sent. |
| `sms_hour_mode_count`      | Count of SMS messages sent during the most frequent hour. |
| `sms_hour_nunique`         | Number of unique hours SMS messages were sent. |
| `sms_day_mode`            | Most frequent day of the month (1st-31st) on which SMS messages were sent. <br> E.g. The most frequent day is the 1st of each month. |
| `sms_day_mode_count`       | Count of SMS messages sent on the most frequent day of the month. |
| `sms_day_nunique`          | Number of unique days of the month SMS messages were sent. |
| `sms_dayname_mode_count`   | Most frequent day of the week SMS messages were sent (Monday - Sunday). |
| `sms_dayname_nunique`      | Number of unique days of the week SMS messages were sent (Monday - Sunday). |
| `sms_rate`                 | Average number of messages per unique contact over 8 months (sms_count / sms_nunique_contact). |
| `sms_contacts_proportion`  | Proportion of unique contacts relative to total SMS messages sent. <br> Close to 1 means interaction with many different contacts. <br> Close to 0 means interactions with the same few contacts. |
| `sms_calltype1_count`      | Count of outgoing SMS messages sent with (`calltype_id = 1`) across 8 months.|
| `sms_calltype2_count`      | Count of incoming SMS messages received (`calltype_id = 2`) across 8 months. |
| `sms_calltype2_proportion` | Proportion of outgoing SMS messages sent (calltype_id = 2) to total SMS messages across 8 months. |

### VOC (Voice Record)

| Feature Name                        | Description |
|-------------------------------------|-------------|
| `imei_count`                          | Number of devices (IMEIs) the phone number was used on across 8 months. <br> International Mobile Equipment Identity (IMEI) is a unique identifier for the device used by the subscriber. |
| `imei_list`                           | List of unique IMEI numbers associated with the phone number. |
| `call_count`                          | Total number of voice call records (incoming + outgoing) across 8 months. |
| `call_unique`                         | Number of unique phone numbers the subscriber has called or received calls from across 8 months. |
| `call_city_unique`                    | Number of unique cities the phone number has made or accepted calls across 8 months. |
| `call_county_unique`                  | Number of unique counties the phone number has made or accepted calls across 8 months. |
| `call_count_mean`                     | Average number of calls made to each unique contact across 8 months. |
| `call_count_median`                   | Median number of calls made to each unique contact across 8 months. |
| `call_count_max`                      | Maximum number of calls made to a single unique contact across 8 months. |
| `call_dur_mean`                       | Average duration of calls across 8 months (in seconds). |
| `call_dur_median`                     | Median call duration across 8 months (in seconds). |
| `call_dur_max`                        | Maximum call duration across 8 months. |
| `call_dur_min`                        | Minimum call duration across 8 months. |
| `voc_hour_mode`                       | Most frequent hour for calls across 8 months. |
| `voc_hour_mode_count`                | Call count during most frequent hour (mode). |
| `voc_hour_nunique`                    | Number of unique hours the subscriber makes/receives calls. |
| `voc_day_mode`                        | Most frequent day of the month for calls (1st-31st). |
| `voc_day_mode_count`                  | Call count on most frequent day (mode). |
| `voc_date_unique`                     | Number of unique days the subscriber makes/receives calls over 8 months. |
| `voc_dayname_mode_count`              | Count of calls made on the most frequent day of the week (mode). (Monday-Sunday). |
| `voc_dayname_unique`                  | Number of unique days of the week the subscriber makes/receives calls across 8 months. |
| `calltypeid_unique`                   | Number of call types used by the subscriber. <br> Call types: Outgoing, Incoming, Transfer. <br> 1 means one type only, 2 means 2 types, 3 means all 3 types. |
| `voc_calltype1_count`                 | Count of outgoing calls (`calltype_id = 1`) across 8 months. |
| `voc_calltype2_count`                 | Count of incoming calls (`calltype_id = 2`) across 8 months. |
| `voc_calltype3_count`                 | Count of transfer calls (`calltype_id = 3`) across 8 months. |
| `voc_calltype1_proportion`            | Proportion of outgoing calls made (`calltype_id = 1`) to total calls across 8 months. |
| `call_outgoing_city_unique`           | Number of unique cities the phone number made outgoing calls to (calltype_id = 1) across 8 months.|
| `call_outgoing_county_unique`         | Number of unique counties the phone number made outgoing calls to (calls with calltype_id = 1) across 8 months. |
| `call_duration_per_contact_median`    | Median total call duration of calls made to each unique contact across 8 months. |
| `call_duration_per_contact_max`      | Maximum total call duration of calls made to each unique contact across 8 months. |
| `call_duration_per_contact_mean`      | Mean total call duration per unique contact across 8 months, calculated as the product of mean call duration across 8 months and call count divided by the unique contacts. |

### USER (Consumption record)

| Feature Name | Description |
|--------------|-------------|
| `arpu_mean`    | Average monthly spending (ARPU) in dollars over 8 months. ARPU (Average Revenue Per User) typically reflects the subscriber's spending behavior on telecom services. |
| `arpu_var`     | Variance in monthly spending. |
| `arpu_max`     | Max monthly spending. |
| `arpu_min`     | Min monthly spending. |
| `arpu_median`  | Median monthly spending. |
| `arpu_sum`     | Total spending over 8 months. |
| `arpu_skew`    | Skewness of spending distribution. |
| `arpu_sem`    | Standard error of the mean (SEM). |
| `idcard_count` | Number of phone numbers registered under the same ID. |
| `label`        | Fraud label: `1 = Fraudulent`, `0 = Non-fraudulent`. |