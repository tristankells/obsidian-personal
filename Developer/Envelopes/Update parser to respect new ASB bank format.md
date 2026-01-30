# Sample
```
Today
AUD 141.67AMAZON MARKETPLACE AUat 0.8644*
–
$163.90
$209.44
Today
Auckland TransportAuckland
–
$30.00
Pending
Yesterday
CARD 5018WOOLWORTHS NZ/100 HALSEYHALSEY STREE
–
$16.17
$373.34
```
# Test Cases
- Date == "Today"
- Date == "Yesterday"
- Balance == "Pending"
	- Should ignore
- Description >= 2 lines
	- Should work with no issue