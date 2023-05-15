
# Social Engineering

Let us first take a look at some common types of spam messages. These are examples right out of the spam folder in one of our email accounts.

* Sample 1 : Canadian Lottery
* Sample 2 : FBI E-Mail 
* Sample 3 : Online Banking

---

### Sample 1 : Canadian Lottery

The first example is a common scam which advertises that the recipient is the winner of the Canadian Lottery.

![image](https://github.com/mohamedabdelhady933/eCPPTv2-Notes/assets/73122852/5e86b4ed-1377-4ace-af0e-0709205f5b6c)

Before opening this attachment, we download and scan it with our local Anti-Virus solution.The scan comes up clean, but we always prefer to be doubly safe, so we also submit it to [Virus Total](http://www.virustotal.com/) for a further
review.Once we know it is clear, we can go ahead and open the attachment, which looks like this

![image](https://github.com/mohamedabdelhady933/eCPPTv2-Notes/assets/73122852/f79e52b7-4965-4850-8e52-6d6217b60d14)


---
### Sample 2 : FBI E-Mail

![image](https://github.com/mohamedabdelhady933/eCPPTv2-Notes/assets/73122852/033f1f38-c80f-42aa-b0e7-c6439b4b2f78)

This says the email came from Mr. Mueller at the FBI. We can verify that, by looking at the message headers in the email.Let’s take a quick look.

![image](https://github.com/mohamedabdelhady933/eCPPTv2-Notes/assets/73122852/58510e84-0584-4045-a04a-9a2dd4522eb2)

According to the headers, the Reply-To: for this message is a paulsmith6@gala.net.That is funny; we thought we were supposed to send our message to paulsmith4@gala.net. Why would the FBI have me contact a guy overseas to give him $200 and my personal information?


---
### Sample 3 : Online Banking

These were just a couple of emails out of my spam folders.Other emails can be even more convincing, as they have bank logos and official looking content, see below:

![image](https://github.com/mohamedabdelhady933/eCPPTv2-Notes/assets/73122852/1fce13d4-c8ad-420a-824d-7c2a3625c50f)

The site that referenced the pictures has been taken down,but, this email had all of the appropriate Bank of America logos when it was first received.However, if you notice where the cursor is pointing, the information at the bottom of the screenshot shows you the associated HTML link.

The link does not go to BOA, but to thesochtimes.com. This is another way that tricksters can fool the unknowing masses: making the link look official but redirecting the victim to a page that is owned by them.The page would look real, but ultimately the person is just giving up their banking information.







