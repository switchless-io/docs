# Intro to bull

## About
We use bull for queue up tasks. Two major reason why we use queues. 

1. something is expected to be heavy and we dont want to block the event loop
2. something is expected to fail and we want the option to retry it

Eg of case 1 is something that heavy process such running some shell scripts or running puppeteer etc. 

Eg of case 2 is a request to be made to a 3rd part that is expected to have a downtime or processing a webhook from a 3rd party system. 

Install bull via switchless cli - https://www.loom.com/share/7da3df9b1df045eba43b5fc66bb0cb70
Basic bull usage walkthrough - https://www.loom.com/share/265833e77edc4651a35240c700f3c68e