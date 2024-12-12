Two factor identification, also known as "2FA" is a security mechanism in which users must supply two different means of authentication to authenticate themselves.  The main purpose of 2FA is to provide an extra layer of security, in order to ensure that attackers have a harder time gaining unauthorized access.

The additional method of authentication may be an OTP (one time password) sent over SMS, e-mail, voice call, or an authenticator application (e.g. Authy, Google Authenticator etc.), a facial/fingerprint scan, a hardware key (e.g. Yubikey, Nitrokey), and such.
https://www.kaspersky.com/blog/types-of-two-factor-authentication/48446/


# Sub-headers from the original repository:
## Response/Status Code Manipulation

Some applications depend on response or status codes to manage behaviour.

When an attacker intercepts and modifies these before they reach the client, the client may respond as if it received a positive response from the server. This is called "Response Manipulation" or "Status Code Manipulation" depending on whether we are modifying HTTP status codes or JSON that we got from the API.
For status codes, we can see if there is any change in the application behavior by modifying 4xx status codes to 200 OK. And for response manipulation, we can modify the JSON value we receive from something negative to something positive which the application expects.

https://medium.com/@security.tecno/response-manipulation-ftw-understanding-and-exploiting-response-manipulation-6ad2d81f2eb4

## 2FA Code Leakage In Response
If, during the authentication phase, the application is written in such a way that it leaks the 2FA code in a response sent to the client, and an attacker is able to intercept the response, the attacker may be able to gain access to the account by abusing the 2FA code.

## 2FA Code Reusability
This vulnerability refers to the scenario where an user was successfully authorized with a 2FA key, but the key was not expired after the authorization. Which means, the key is still usable, and an attacker that has gained access to the key is able to gain access to the resource.

## Lack of Brute-Force Protection
If there is no protection against brute forcing, we can simply try every combination until we hit the right one. That means, it should be possible to brute force the 2FA code with a tool like Burp Intruder.

Example lab:
https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-bypass-using-a-brute-force-attack

## Password Reset / Email Change - 2FA Disable
If we are able to get the user to change their password or email, 2FA gets disabled, and this may cause a security problem.

## Missing 2FA Code Integrity Validation

In this scenario, we are able to use the valid 2FA code we received for our own account, for the authentication of the other account that we intend to access, as the program only checks if the code is valid, not whether the code belongs to the account it is being used for.

## Clickjacking / CSRF on 2FA page
!TODO: explain clickjacking and csrf


## Previously created sessions aren't terminated after 2FA is activated

In this scenario, enabling 2FA does not automatically terminate every session of an user, so any other device that's still logged in will be able to continue accessing the resource. This may be a problem if an attacker has access to a session, as enabling 2FA will still let them act in an unimpeded manner.
https://hackerone.com/reports/1927360
## Bypass 2FA with null or 000000

In this scenario, upon receiving an OTP for 2FA, an attacker may be able to bypass authentication by sending 000000 or adding a null character to the POST request, and successfully logging in.
https://hackerone.com/reports/897385




Some resources I have used:
https://github.com/daffainfo/AllAboutBugBounty/blob/master/Bypass/Bypass%202FA.md
