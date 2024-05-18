# Phishing

## Idea

Since the task is to retrieve either Bob's or Alice's password, and we were given the following information:

- Bob has a dog (a bull terrier) named "Shimi," and he really loves his dog.
- Alice is a fan of mechanics. She has two vintage cars and often likes to parade around with her antique items.

I chose to target Bob, using the information that he loves his dog.

Given that this is a simulation and not real life, I assumed that Bob has an Instagram account where he posts pictures of his dog, under the username 'BobXShimi'. Thus, I decided to target him with an Instagram phishing email. The email would state that a fellow dog lover has started following him, enticing him to click the link and attempt to log in on a fake Instagram login page.

## Gophish 

### What is Gophish ?

https://github.com/gophish/gophish

Gophish is an open-source phishing simulation and security awareness training tool designed to help organizations assess and improve their susceptibility to phishing attacks. It allows security professionals to create and send customized phishing emails to employees, track the responses, and analyze the results to identify areas where additional training might be needed. Here are some key features and uses of Gophish:

#### Key Features

1. **Phishing Campaigns**: Gophish allows users to create and manage multiple phishing campaigns. These campaigns can be tailored with custom email templates and landing pages to closely mimic real phishing attacks.
    
2. **User-Friendly Interface**: The platform provides an intuitive web-based interface where users can easily set up and launch phishing campaigns without needing extensive technical knowledge.
    
3. **Email Templates**: Users can create their own phishing email templates or use pre-made ones. These templates can include various phishing techniques, such as attachments, links, and embedded images.
    
4. **Landing Pages**: Gophish enables the creation of realistic landing pages where users are directed after clicking on a phishing link. These pages can collect data such as login credentials to simulate real-world phishing scenarios.
    
5. **Tracking and Reporting**: The tool tracks who received the emails, who opened them, who clicked on links, and who submitted information on landing pages. Detailed reports and analytics help organizations understand their employees' behavior and vulnerabilities.
    
6. **Modular Design**: Being open-source, Gophish can be customized and extended to meet specific needs. Users with programming skills can modify the source code to add new features or integrations.
    

#### Uses

1. **Security Awareness Training**: Organizations use Gophish to train employees on how to recognize and respond to phishing attacks. By simulating real phishing attempts, employees can learn in a safe environment.
    
2. **Risk Assessment**: By analyzing how employees interact with simulated phishing emails, organizations can identify individuals or departments that may require additional training or intervention.
    
3. **Compliance**: Regular phishing simulations can help organizations meet regulatory requirements for cybersecurity training and awareness.
    
4. **Incident Response Preparedness**: Simulated phishing attacks can also test and improve an organization's incident response procedures, ensuring that staff know how to react to a real phishing attack.
    

#### Advantages

- **Cost-Effective**: As an open-source tool, Gophish can be a more affordable option compared to commercial phishing simulation services.
- **Customizable**: Users can tailor the tool to their specific requirements, making it flexible for various types of organizations and security needs.
- **Community Support**: Being open-source, Gophish benefits from a community of users and developers who contribute to its improvement and share best practices.

### How to install Gophish ? 

To install Gophish on your system, follow these steps:

1. Visit the [Gophish releases page](https://github.com/gophish/gophish/releases/) and download the appropriate version for your system.
2. Unzip the downloaded file into a directory named "Gophish".
3. Launch Gophish by running the executable file.

Upon your first launch, the password for the admin user will be displayed in the console. You will be prompted to change this password on your first login.

To host Gophish online, modify the `listen_url` part in the `config.json` file to `"0.0.0.0:3333"`.

```
mkdir Gophish
cd Gophish
wget <link>
unzip gophish-file
nano config.json ( modify "listen-url":"0.0.0.0:3333")
sudo chmod +x gophish

```


### How did I configure my Gophish campaign ? 

#### Users & Groups

![Gophish Users & Groups](/assets/gophish-users.png)

You can either create users manually or importing a CSV file to import lots of users at the same time.

#### Sending Profile

![Gophish Sending Profile](/assets/gophish-sender.png)

Unless you use a less restrictive smtp server than the mainstream ones, you have to input your real mail address between the brackets in the SMTP From field. 

For the host, as I used outlook it is : smtp-mail.outlook.com using the 587 port, but if you used google for example it would have been : smtp.gmail.com using the same 587 port. It needs to be changed depending on the smtp service that you want to use so I recommend that you make a quick google search for it.

For the username and password, use your email address and the corresponding password for the email service. Depending on the service, you may need to use an app-specific password.

#### Email Template

Now that you have configured a user to receive your mails and a profile to send your mails, you need an email template to send. 

![Gophish Email Template](/assets/gophish-mail.png)

This is where you need to start being creative. 

Since I wanted to make an instagram phishing e-mail, I went to my old e-mail address and copied the html code of an instagram e-mail that I once received.

Most images were blank and/or outdated so I had to change most src links in the html to craft the mail. 

#### Landing Pages

![Gophish Landing Page](/assets/gophish-landing.png)

Gophish has a feature that allows you to import websites, although its effectiveness depends on the complexity of the page you wish to copy. Often, you will need to edit the login form to ensure it functions correctly.

Additionally, you can choose whether to capture the data that your target inputs and specify a page to which the user will be redirected.

For my Instagram phishing page, I found a template [here](https://github.com/rat-c/gophish-templates/blob/main/landing/instagram.html) and modified the form to make it compatible with Gophish.

#### Campaign

![Gophish Campaign](/assets/gophish-campaign.png)

Once everything is setup, you can start your first campaign !

The user receives this e-mail : 

![Gophish Mail](/assets/gophish-mail-received.png)

If the user clicks on it he goes to this page : 

![Gophish Instagram Landing Page](/assets/gophish-insta.png)

And you will retrieved the data on the dashboard :

![Gophish Retrieved Data](/assets/gophish-dashboard.png)

## Disclaimer

The content provided in this report is intended solely for security awareness and educational purposes. The demonstrations and techniques described are designed to help individuals and organizations understand the nature of phishing attacks and to improve their security posture against such threats.

**Phishing is illegal and unethical.** Unauthorized phishing activities can cause significant harm, including identity theft, financial loss, and damage to reputations. Engaging in phishing attacks without explicit permission from all affected parties is a violation of law and can result in severe legal consequences.

This report and the associated demonstrations using Gophish are created to educate users on how to recognize and defend against phishing attempts. They should **not** be used to conduct unauthorized activities or to target individuals or organizations without proper authorization.

Always conduct security testing within legal boundaries and with the explicit consent of those involved. The author of this report and the developers of Gophish do not endorse or condone any illegal or unethical activities and are not responsible for any misuse of the information provided.

By using the information and tools discussed in this report, you agree to use them responsibly and in accordance with all applicable laws and regulations.
