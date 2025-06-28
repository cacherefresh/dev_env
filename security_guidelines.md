#### Security Guidelines

Remeber these are guidelines - every situation is different. use the most up to date and check with your security team of their special needs, integrations or requirements. 
FIPS, SOC 2 Compliance, HIPAA, Gov Cloud, ITAR restrictions etc. 

Some good things to remember:

encrypt the harddrive. 
with windows + wsl encrypt the entire wsl, always use a password that isnt blank, same with the git ssh keys. 
when you use wsl2, YOU MUST SETUP YOUR OWN FIREWALL - WSL runs bypassed by windows defender, so do not rely on it for antivirus, can't tell you how many companies had NO ANTIVIRUS on wsl setups that were not running iptaples or similiar. 

setup universal firewall if they ever get it to work, fall back on iptables if they haven't
encrypt the wsl distro, AND inside encrypt your ssh keys inside your wsl. remember bitlocker encyption is for when you lose a laptop, not for when you have already unencrypted and are using it. 
sign any distro to your tpm
isolate your development distro with encrypted ssh keys inside the encrypted wsl distro.  only spin up the flavor of wsl linux distro you are using. you dont want a vulnerable distro running legacy java jdk/jvms or nodejs packages or chocaltely running with rogue packages.
Personally I just buy new computers, but not everyone has that ability. so keep the host operating system clean clear up to date and secure. NO DEVELOPMENT in WINDOWS if you arnt using multiuple computers. 

Store your keys with a yubi key or something similiar, always use 2fa (two factor auth) and get yourself an encrypted keyfile password manager. do not rely on apple keychain and firefox alone. have it clear your ctrl+c after time expiry.

