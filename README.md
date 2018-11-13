# SharedSpheres - AR Multiplayer Experience

We want to showcase an example of two or more devices being able to share an augmented reality experience in the same space.

ARKit 2 introduced the notion of **ARWorldMap** which allow you to share your coordinate space with another device while interacting in AR.  We use [Unity ARKit Plugin]() to interact with ARKit 2 SDK, but we needed a mechanism to transmit the ARWorldMap between devices.  

The solution for local multiplayer we settled on for this example is [CaptainsMess](https://github.com/hengineer/CaptainsMess) by the inimitable **Spaceteam**.  

（補足）<br>
↑Spaceteamってなんだよって気持ちになりますが、たぶん[これ](http://teban.pico2culture.jp/article/61303993.html)のことです。

Spaceteam is a free-to-play local cooperative multiplayer video game developed and published by Henry Smith of American studio Sleeping Beast Games for iOS and Android operating systems. It was released on December 1, 2012.[1] and is described as a "cooperative shouting game for phones and tablets".[2] The game uses multiple smartphone or tablet devices, connected via wifi or bluetooth, to enter a shared game of up to two to four players.<br>
↑[SpaceteamのWikipedia](https://en.wikipedia.org/wiki/Spaceteam)より<br>
（補足終わり）

This app is created with a combination of the two projects mentioned above.  We start off with a scene that maps the area around your device to obtain the ARWorldMap for the area you are going to play in.  

Then we go to a scene which contains the lobby (as implemented by CaptainsMess example) so that we can connect up the devices.  You can choose to autoconnect or choose one device to be the host and others to be clients. Once they are connected, the host device will send its **ARWorldMap** to all the clients, who will all relocalize to the host device's coordinate system.  

Since the **ARWorldMap** can be hundereds of kilobytes, and UNet does not have a mechanism to transmit large messages or files like that, we divvy them up into smaller chunks using a mechanism found [here](https://answers.unity.com/questions/1113376/unet-send-big-amount-of-data-over-network-how-to-s.html).  

We also implement a sphere prefab that is registered by UNet so that it can be spawned on all clients at the same time.  Then when we press a button on one client, it generates a sphere prefab of a certain color which is different from the color of the spheres generated by other clients.

Go check it out!

