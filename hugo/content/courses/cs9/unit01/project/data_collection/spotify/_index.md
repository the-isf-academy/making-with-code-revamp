---
title: [Spotify Data]
type: checkup
---
# Spotify
*It is important that you don't put off this task, as the download request can take up to 30 days to be fulfilled. You could end up without any data to work with!*

---

## Downloading Data

[0] **Login.** Navigate to [spotify](https://open.spotify.com/) in your browser. Log in if necessary.

[1] **Account.** Select your profile dropdown and click on `Account`


{{< figure src="images/courses/cs9/unit01/spotify_download_step1.png" width="100%" >}}

[2] **Privacy Settings.** On the Account overview page, scroll down and click `Privacy Settings`

{{< figure src="images/courses/cs9/unit01/spotify_download_step2.png" width="100%" >}}

[3] **Request.** At the very bottom of the Privacy page, you can request your data. Click `Request`.
{{< figure src="images/courses/cs9/unit01/spotify_download_step3.png" width="100%" >}}

[4] **Confirmation Email.** An email has been sent to confirm the request. If you have access to the email address for the account, click `Confirm`. If you don't, ask the account owner to confirm the request for you.

{{< figure src="images/courses/cs9/unit01/spotify_download_step4.png" width="100%" >}}

[5] **Finished.** Once you've confirmed via email, you should see this banner on the Privacy settings page of your account. That means you're all set!
 {{< figure src="images/courses/cs9/unit01/spotify_download_step5.png" width="100%" >}}

---

## Get Client ID, Client Secret, and Add URI

{{< code-action "Follow along with this video and the steps below to create a Spotify Client ID and Client Secret." >}}

<br>
<br>


{{< youtube "or6GSvjmyyE" >}}

> 0. **Go to [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/login).**
> 0. **Scroll down and select `LOG IN`.** This will trigger a pop-up that may prompt you to enter your Spotify credentials.
> 0. **Select `CREATE AN APP`**
> 0. **Fill in the form and click `CREATE`.** The App name and App description can be whatever you would like.
> 0. **Click `SHOW CLIENT SECRET`**
> 0. **Copy both the `Client ID` and `Client Secret`**

{{< code-action "Follow along with this video and the steps below to add in your Redirect URI." >}}

{{< youtube "B_NYjslAGfw" >}}

> 0. **On the same [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/login), click on `EDIT SETTINGS`**
> 0. **Paste http://127.0.0.1:9090 into the *Redirect URIs* field**
> 0. **Select `ADD`**
> 0. **Scroll down and click `SAVE`**
