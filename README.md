# bug-and-arts
Articles on how to prank a snork, obtain an artifact, and other joys of pentest

# A Graceful Attack: SQL Injection through XSS Flaw in Contact Form 7 #

## Introduction ##

In the realm of cybersecurity, there are always those who can turn a vulnerability into a doorway leading to unprotected reservoirs of data. In the Contact Form 7 plugin for WordPress, not only has a reflected XSS vulnerability been discovered (CVE-2024-2242), but there's also a unique opportunity to execute SQL Injection, much like a series of deceitful masks swapping places in a single masquerade. Let’s unveil the cards:
Nuances of Exploitation: SQL Injection via XSS

At first glance, the XSS vulnerability in this plugin seems blatantly typical: a user input element, lacking proper filtration, suddenly appears on screen, enhancing HTML, enabling attacks on an administrator via the link: https:///wp-admin/admin.php?page=wpcf7&post=$FORMID&active-tab=1%22%3E%3Csvg%2Fonload%3Dalert%281%29%2F%2F%3E. However, in the intricate play of shadow and light, the XSS vulnerability opens the door to deeper manipulations for a hacker. Since special characters don't undergo proper sanitization, it allows for discreet exfiltration of the entire database from the site.
Theatrical Staging of the Attack and Participants:

    Setting the Scene:
        It all begins with a simple parameter in a GET request. The potential of XSS here is merely the tip of the iceberg.

    The Hidden Passage:
        The parameter active-tab1, along with the AND boolean-based blind - WHERE or HAVING - subquery comment (white string =), possesses the capability to become an SQL Injection. An attacker can inject it gracefully, like an invisible needle piercing the fabric of security systems and WAF.

    Climax:
        Through the enumeration of other, more complex SQL Injection queries, the attacker reaches the very essence of SQL Injection (it is recommended to use sqlmap for this purpose).

Protecting the Stage: Preventing a Double Game

To avoid becoming a hostage to the XSS vulnerability once again, it is necessary to close this vulnerability:
Measures of Escaping and Data Validation:

Always use escaping; if not possible, block the vulnerable parameter on the WAF from external access.
    Use in code:

    php

Copy code

    sanitize_text_field($_GET['active-tab1']));

Multiplying Defense Mechanisms:

    Integrate Wordfence and other similar tools.

## Final Aria ##

This story is a reminder of the constant vigilance and study of the art of cybersecurity, which sometimes resembles the choreography of a waltz between vulnerabilities and protective mechanisms. Strive for mastery in this game of light and shadow, where each vulnerability can become decisive in the entire play.
Sources of Inspiration:

    Download CVE-2024-2242
    WPScan Report
    Wordfence Opera

Thus, do not forget to seek light and harmony, and study the exquisite art of protecting your digital realms.
