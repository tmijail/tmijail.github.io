---
title: "Debugging Odoo computed field with `ir.logging`"
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
log = dict(
	type='client',
	name='my_compute_field',
	path='n/a',
	line='n/a',
	func='n/a',
	message=' '
)

for rec in records:
  # [...]

  log['message'] = "Hello from the computed field"
  logging.create(log)

  # [...]

  log['message'] = "value: " + str(rec.value)
  logging.create(log)

  # [...]
```