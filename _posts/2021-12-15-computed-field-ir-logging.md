---
title: "Debugging Odoo compute fields with `ir.logging`"
categories:
  - Tips
tags:
  - Odoo
---

I was trying determine why a computed field wasn't working as expected and was really annoyed at the fact that `log` isn't available on that context. 
We can create a record on the `ir.logging` table, though.

(Tested on V13)
```python
logging = self.env['ir.logging']
def log(msg, logging=logging):
	logging.create(dict(
		type='client',
		name='my_compute_field',
		path='n/a',
		line='n/a',
		func='n/a',
		message=str(msg)
	))

for rec in records:
  # [...]

  log("Hello from the computed field")

  # [...]

  log(rec.value)

  # [...]
```