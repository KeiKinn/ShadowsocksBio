## Preface
The China National Firewall (unofficially), is a collection of software and hardware systems that manage inbound and outbound network traffic in China. It is known among Chinese internet users as the "Great Firewall" (GFW). Due to the GFW, access to foreign websites such as Google, Twitter, and Facebook is restricted within mainland China, as the GFW can selectively block foreign websites, effectively dividing the internet into two separate systems - a domestic internet and an international internet. In most cases, "the Wall" refers to the GFW.

There are many ways to bypass the GFW. Here is a brief overview of some classic and new methods:

### Classic methods
- Modify the computer's host file: By manually specifying the IP addresses of relevant websites, this method can bypass DNS and achieve the goal of climbing over the wall. Although it is the simplest and most direct method, it still exists, and there are software projects that regularly update the host list.
- Forcefully specify the system DNS: One of the main attack methods of the GFW is DNS pollution, so forcing the system DNS is a way to avoid returning invalid IP addresses. This method is often used in conjunction with Method 1.
- VPN: Originally used as an anonymous, secure, and confidential VPN service, it has been discovered to have the potential for climbing over the wall. The principle is relatively simple: select a server that has not been blocked by the GFW and use it to forward the traffic of relevant websites to your device. The communication between the device and the VPN server is not within the range of the GFW's blocking, thus achieving the goal of climbing over the wall. VPN was originally designed for enterprise services, allowing employees to remotely log in to the company's intranet for operations. The main protocols include PPTP, L2TP, IPsec, IKEv2, and OpenVPN, among others.
- A series of network services such as GoAgent, FreeGate, and fqrouter.
### New methods
-Shadowsocks-like: This mainly includes various versions of Shadowsocks derivatives, such as ShadowsocksR and Shadowsocks-libev. The feature of this method is that it encrypts the data during communication and routes the traffic.
- Intranet penetration: A typical example is ZeroTier, which establishes a relay management server. Clients that join the server are equivalent to being in the same LAN. Not only can they climb over the wall, but they can also achieve multi-device linkage within the virtual intranet. ZeroTier has a public server called Earth, and users can also build their own ZeroTier relay servers, called Moon by the official.
- V2Ray: V2Ray is a tool under Project V. Project V is a project that includes a series of tools to build specific network environments. V2Ray is the core of the project. The official introduction of Project V provides a single kernel and multiple interfaces. The kernel (V2Ray) is used for actual network interaction, routing, and handling of network data, while the peripheral user interface program provides a convenient and direct operation process. However, in terms of time, V2Ray came before Project V. Today, the developer of V2Ray has gone missing, and the development and maintenance work of V2Ray has basically stalled.
- Great Weapon: It's a strange name, seemingly developed by an interesting person. I have not paid attention to it personally.

## Shadowsocks
## A brief history
On April 22, 2012, a user named "clowwindy" on V2EX shared a tool that he had been using for over a year to bypass Internet censorship, called **Shadowsocks**.

![](image/cwpostss.png)

In essence, Shadowsocks is an encryption protocol that obscures the destination address and content of network data, making it difficult for the Great Firewall (GFW) to detect and block unwanted traffic. Unlike traditional VPN technology that routes all traffic through a VPN server, Shadowsocks uses a configuration file (PAC) to implement network routing, allowing users to specify which websites to proxy and which ones to access directly. This greatly improves browsing performance and allows users to access blocked content without relying on the VPN server's location.

Shadowsocks quickly gained popularity among developers and users due to its flexibility and ease of use. It inspired the creation of various implementations in different programming languages and clients on major platforms. People were passionate and enthusiastic about contributing their expertise and ideas to the development of Shadowsocks.

At the time, traditional VPN services were able to cope with the immature GFW, while Shadowsocks was still a fragile and thriving young bud, quietly absorbing nutrients and waiting for the right time to bloom.

The initial Shadowsocks clients came with built-in node information, and some people shared their own nodes online. Although the speed was slightly slow and the stability was not good, they were still a good option for ordinary users who didn't need to configure anything extra. For those with the demand and technical expertise, they could set up their own Shadowsocks servers on their own servers. The only regret was that iOS at the time did not have network access permissions. Users either had to use the limited Shadowsocks browser for bypassing restrictions, or jailbreak their devices to install the Shadowsocks client and take over the network to enable Shadowsocks proxy.



## Winter is coming

**On August 20, 2015**, Clowwindy posted the several sentences on GitHub:

>Two days ago the police came to me and wanted me to stop working on this. Today they asked me to delete all the code from GitHub. I have no choice but to obey.
>
>I hope one day I’ll live in a country where I have freedom to write any code I like without fearing.
>
>I believe you guys will make great stuff with Network Extensions.
>
>Cheers!

That night, Clowwindy closed all the Issues panels in several Shadowsocks code repositories he maintained, deleted all help information, and changed all descriptions to "Something happened". At the same time, he also cleared the membership of these repositories/organizations, or transferred all members to private status, not publicly visible.

There was an air of unusualness.

**On August 21, 2015**, news began to spread online that Clowwindy had been invited for tea (a euphemism for being interrogated by authorities). Later, Clowwindy replied to issue #305 of Shadowsocks-Windows, saying:

> I was invited for some tea yesterday. I won’t be able to continue developing this project.

At the same time, he enabled Twitter's privacy protection feature, which prevented anyone who wasn't already following him from viewing his tweets.

That night, Clowwindy posted a tweet with the word "thanks" to indicate that he was safe and sound.

![](image/cw.png)

### Some words followed

Clowwindy's experience did not completely extinguish the passion of all developers, so the subsequent development and maintenance work did not stop. A lot of things happened during this uncertain period, which can be quite confusing. We won't go into the details of the causes and consequences here.

The author of ShadowsocksR, Breakwa11, is a highly controversial figure. She took over the development work of Shadowsocks after Clowwindy's departure, but violated the open-source agreement by closing the source code. She also implied in her release that she was the original author. Clowwindy made some responses to this in issue #108 of shadowsocks-windows (https://github.com/shadowsocks/shadowsocks-windows/issues/293#issuecomment-132253168):

>那是自然的咯。这边加了什么功能，它（SSR）马上扒过去合并了。它那边加了什么却不会贡献出来给其他人用，久而久之，不就是它那边功能更多了吗。
>
>That's natural. If we added a new feature here, then SSR would quickly copy it and merge it into their own code. But if they added a feature on their side, they wouldn't contribute it back to the community for others to use. Over time, this would mean that their version would have more features.

>一直以来我什么都没说是因为我对他还有点希望，所以得给他一点面子不是。一开始我还只是纳闷他为什么不发 pull request，过了一段时间我才明白，这个世界上也有这一类的人。不尊重 GPL 就算了，把作者名字换成自己的，还在主页上加上官方的字样。为什么我们这边反而不说官方呢？因为我希望这个项目是没有官方的，人人都是贡献者。想不到这个社会人人都围着官转，人人都巴不得当官 。
>
>I haven't said anything all along because I still had some hope for him, so I wanted to preserve basic respect and decency for him/her. At first, I just wondered why he/she didn't submit a pull request, but after a while, I realized that there are people like that in this world. Not only did he/she not respect the GPL, he/she also changed the author's name to his own and added the word "official" to his homepage. Why don't we use the word "official" on our side? Because I hope this project have no such called official things, and everyone could be a contributor. I didn't expect that in this society, everyone revolves around officialdom, and everyone wants to be an official deadly.

>既然他没有尊重别人劳动成果的意愿，那他那些不开源的理由想必也只是借口。说因为加了一些试验性功能会不兼容所以暂不开源。他弄了一个混淆 TCP 协议头功能，在界面上标注提升安全性，吸引用户打开，然后安装他自己的不兼容服务端。然而我分析了一下之后发现这个功能的设计就是想当然，用得多了以后反而会增加特征。如果你真有什么试验性功能，不是更应该开放出来让所有人帮你分析么，大家一起讨论么？在加密算法领域，只有经过足够多人和机构的审视的算法，才能视作是安全的，闭门造出来的怎么能用。。
>
>Since he/she has no intention of respecting the labor achievements of others, his/her reasons for not open sourcing are probably just excuses. He/She said that because he/she added some experimental functions that may be incompatible, he/she will not open source them for the time being. He/She made a function of obfuscating the TCP protocol header, marked it as improving security on the interface, and attracted users to turn it on, and then installed his own incompatible server. However, after analyzing it, I found that the design of this function was based on assumptions, and it would actually increase features after being used more. If you really have any experimental features, shouldn't you open them up for everyone to analyze and discuss together? In the field of encryption algorithms, only algorithms that have been scrutinized by enough people and institutions can be considered secure, and how can those developed behind closed doors be used?

>当然啦，大部分用户才不会管这些，他们不会分析你是不是真的安全，也不会做道德判断，只要他们觉得好用就行。所以可以看到，这种环境下开源其实并没有什么优势，只不过为一些人抄袭提供了便利。这种环境下最后留下来的都是这些人。
>
>Of course, most users don't care about these things. They won't analyze whether you are truly secure, nor make moral judgments. They just want something that works well. So you can see that in this environment, open source doesn't really have any advantages, it just makes it easier for some people to copy. In this environment, the only ones left in the end are those people.

>我一直想象的那种大家一起来维护一个项目的景象始终没有出现，也没有出现的迹象。维护这个项目的过程中，遇到 @chenshaoju 这样主动分享的同学并不多。很多来汇报问题的人是以一种小白求大大解决问题，解决完就走人的方式来的，然而既不愿提供足够的信息，也不愿写一些自己尝试的过程供后人参考。互帮互助的气氛就是搞不起来。对比下国外的社区差好远。
>
>I have always imagined the scene where everyone comes together to maintain a project, but it has never appeared, nor is there any sign of it. In the process of maintaining this project, there are not many pals like @chenshaoju who actively share. Many people who come to report problems come in a way of seeking help from experts as a novice, and they leave after the problem is solved. However, they are unwilling to provide sufficient information or write down the process they tried for later reference. The atmosphere of mutual assistance just cannot be created. Compared to foreign communities, ours is still far behind.



>最适合这个民族的其实是一群小白围着大大转，大大通过小白的夸奖获得自我满足，然后小白的吃喝拉撒都包给大大解决的模式。通过这个项目我感觉我已经彻底认识到这个民族的前面为什么会有一堵墙了。没有墙哪来的大大。所以到处都是什么附件回帖可见，等级多少用户组可见，一个论坛一个大大供小白跪舔，不需要政府造墙，网民也会自发造墙。这尼玛连做个翻墙软件都要造墙，真是令人叹为观止。这是一个造了几千年墙的保守的农耕民族，缺乏对别人的基本尊重，不愿意分享，喜欢遮遮掩掩，喜欢小圈子抱团，大概这些传统是改不掉了吧。
>
>The most suitable for this nation is actually a group of novices surrounding an expert, and the expert gains self-satisfaction through the praises of the novices, while the novices rely on the expert to solve all their problems, including their basic daily needs. Through this project, I feel like I have thoroughly understood why there is a wall in front of this nation. Without the wall, there would be no such expert. So everywhere you go, you see things like "attachments visible after replying" and "user groups with certain levels can view", a forum with an expert for novices to worship. They even fxxking build a wall for developing a proxy software. It is truly astonishing. This is a conservative agricultural nation that has built walls for thousands of years, lacking basic respect for others, unwilling to share, and preferring to cover up and form small circles. Perhaps these traditions cannot be changed.

>现在维护这些项目已经越来越让我感到无趣。我还是努力工作，好好养家，早日肉翻吧。
>
>Now maintaining these projects has become more and more boring for me. It is much better for me to work hard, support my family well, and get out of here as soon as possible. ( “get out of here” is a slang term that means “to leave one’s country by physical means”)

## The Sudden Death of SSR

Controversy has always existed, but this has not stopped the progress of SSR. More and more people are turning to SSR, and SS is gradually falling behind, but there is also a group of supporters. Beneath the calm surface, there are turbulent undercurrents, and the moment of eruption has already passed. Whether the encounter of developer breakwa11 is true or false, it is equally chilling.

On July 19, 2017, breakwa11 forwarded the Shadowsocks protocol detection results in Shenzhen on the Telegram channel "ShadowsocksR news", which was forwarded by a large number of users and caused panic.

On July 27, 2017, breakwa11 was attacked by an unidentified person claiming to be "ESU.TV". They claimed that if he did not stop developing and prevent users from discussing this event, more personal privacy information would be released. Later, breakwa11 stated that he was the target of doxing, and the personal information that they made public was completely irrelevant to him. It was just information he randomly filled out at the time. To prevent they from continuing to harm unrelated people, breakwa11 decided to delete all the code on GitHub, dissolve the relevant communication groups, and stop the ShadowsocksR project. He posted the following message on Telegram:

> This doxing incident has made me seriously doubt whether it is right for me to do SSR. First of all, regardless of whether the information is correct or not, from the behavior point of view, someone wants me to die, wants this project to die, and hates someone to such an extent. I know that I am very pretentious, so I have offended many people, especially recently I publicly raised the issue that Shadowsocks can be detected, which has made many people indignant and determined to get rid of me. Although from my perspective, I just hope to raise attention and promote modifications on the Shadowsocks side. This does not mean that I want Shadowsocks to die. Haven't all the issues I raised been improved, including OTA and AEAD? I also participated in the design of AEAD, you can ask Syrone Wong, and NoisyFox can confirm it. Moreover, I also participated in the modification of a part of Shadowsocks-windows. However, now that I have looked at the doxing information, it is really chilling. They even pulled out the other party's Alipay transaction records. Is this really okay? I do not want to harm another person because of my own problems. I hope to make a deal with those who oppose me. I can stop developing SSR in exchange for deleting the project and related things and never appearing again. The SSR group will be dissolved, the account will be cancelled, and the code will be deleted. For me, this project is just something I use to prove my own ideas. It is dispensable, and the production is just for interest. There is nothing to regret about throwing it away. There are so many substitutes, and I am not necessary. You always say that I am attracting fans. You really think too much. There is no need for this. If this can exchange for another person to be free from online violence, I also think it is worth it. On the contrary, if the result of doxing is still made public, then my behavior cannot save it. Then I can continue to develop SSR. But it won't be too long, probably no more than a year before I graduate. Thank you for your support over the past two years. Tonight at 12 o'clock, with the dissolution of the SSR group as a sign, if it dissolves, then I will officially say goodbye to everyone.

At 12 o'clock that night, breakwa11 disbanded the Telegram group.

Thus, the author of SSR withdrew.

## Inheritance

The encounter and subsequent exit of clowwindy and breakwa11 actually implies the growth of the GFW. It is not just a technological game, but its concept is beginning to expand into broader fields. Technology always has loopholes that can be continuously filled, but it is difficult to fix the developer's own loopholes. It not only needs to solve problems but also needs to solve the root cause of the problem.

Thanks to clowwindy's decision to open source Shadowsocks, a large number of forks have kept Shadowsocks up-to-date. According to the current results on GitHub, Shadowsocks on various platforms (even routers) is still constantly being updated, with major feature updates and new issues being submitted. Every drop of small power is pushing the project forward, but its future is still unknown.

The surging tide will recede, but the next time, the next time, it will still gather strength and surge forward, which is the beautiful expectation I hold. However, since 2018, the development of various protocols has actually entered a bottleneck, and it seems to have reached a certain balance in the game with GFW. The whole community can feel that it is no longer focusing on core encryption and feature hiding. More developers are putting their thoughts on airport services (that will provide different VPN severs at the same time). In a sense, the power that Shadowsocks has aroused in the technical field has entered a period of dormancy, which is equivalent to taking the blue pill.

## The plot thickens

### Tightened Control

At the end of July 2017, several VPN-related applications on the China App Store were suddenly removed without any explanation or notification. Users who had already purchased these applications were unable to download them from their purchased items, indicating that Apple's removal directly blocked all channels for downloading from the China App Store. Apple's response was:

> We have received a request to remove some non-compliant VPN apps in China. These apps are not affected in other markets.

The so-called regulations referred to in the response were the "Notice on Cleaning up and Standardizing the Internet Network Access Service Market" issued by the Ministry of Industry and Information Technology in January 2017, which clearly stated:

> The standard applies to enterprises or individuals who have not obtained the qualifications for international communication business, rent international dedicated lines or VPNs, and conduct cross-border telecommunications business activities without the approval of the telecommunications regulatory authority. For foreign trade enterprises and multinational enterprises that need to connect to the Internet across borders for office use, they can rent from telecommunications service operators that have set up international communication entry and exit offices in accordance with the law. The relevant provisions of the "Notice" will not have any impact on their normal operation.

Affected by this, many users could only contact the developers, and many developers could only distribute updates to users through TestFlight. However, because apps distributed through TestFlight expire after 90 days, once the developer stops updating, users will no longer be able to use the software. This risk has also led many users to register for an Apple ID in another region and repurchase the application. Since filing is required by the Ministry of Industry and Information Technology, and individuals do not have the qualifications for filing, it basically means that the removed applications cannot be reinstated. This incident has also received widespread attention and criticism from the international community, and the only consolation is that Apple's removal of the software has forced the government to introduce corresponding clear rules.

In October 2017, with the opening of the 19th National Congress, a large number of routes were blocked, especially SSR. Major airports and Telegram groups were all lamenting. Fortunately, many IPs were unblocked after the congress closed, but the specific ratio is unclear.

During the January 2018 and subsequent "Two Sessions" periods, a larger-scale IP blocking was implemented, covering a wider range and involving various algorithms for circumventing the Great Firewall. Some users reported on Shadowsocks' Issues that their freshly set up server was blocked within just a few minutes.

On September 30, 2018, the Ministry of Public Security issued a [Regulation on Internet Security Supervision and Inspection by Public Security Organs]((http://www.mps.gov.cn/n2254314/n2254409/n4904353/c6263180/content.html)), which was passed at the Ministerial Office Meeting of the Ministry of Public Security on September 5, 2018, and will be implemented from November 1, 2018.