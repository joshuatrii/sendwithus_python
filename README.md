sendwithus python-client
========================

## status
BETA - this client implements v1_0 of SWU API and is functional and tested

## requirements
python requests library

## installation
	pip install sendwithus

## to run tests
	python setup.py test 

## usage

### Call with REQUIRED parameters only
The `email_data` field is optional, but highly recommended!

```python
import sendwithus
api = sendwithus.api(api_key='YOUR-API-KEY')
r = api.send(
    email_id='YOUR-EMAIL-ID',
    recipient={'address': 'us@sendwithus.com'})
print r.status_code
# 200
```

### Call with REQUIRED parameters and email_data
```python
import sendwithus
api = sendwithus.api(api_key='YOUR-API-KEY')
r = api.send(
    email_id='YOUR-EMAIL-ID',
    recipient={'address': 'us@sendwithus.com'},
    email_data={ 'first_name': 'Matt' })
print r.status_code
# 200
```

### Optional Sender
The `sender['address']` is a required sender field

```python
r = api.send(
    email_id='YOUR-EMAIL-ID',
    recipient={ 'name': 'Matt',
                'address': 'us@sendwithus.com'},
    email_data={ 'first_name': 'Matt' },
    sender={ 'address':'company@company.com')
print r.status_code
# 200
```

### Optional Sender with reply_to address
`sender['name']` and `sender['reply_to']` are both optional

```python
r = api.send(
    email_id='YOUR-EMAIL-ID',
    recipient={ 'name': 'Matt',
                'address': 'us@sendwithus.com'},
    email_data={ 'first_name': 'Matt' },
    sender={ 'name': 'Company',
                'address':'company@company.com',
                'reply_to':'info@company.com'})
print r.status_code
# 200
```

### Optional CC
The `cc` kwarg expects a list of dictionaries, where `address` is required
and `name` is optional

```python
r = api.send(
    email_id='YOUR-EMAIL-ID',
    recipient={ 'name': 'Matt',
                'address': 'us@sendwithus.com'},
    email_data={ 'first_name': 'Matt' },
    cc=[
        {'name': 'CC Name', 'address': 'ccaddress@company.com'},
        {'name': 'CC 2 Name', 'address': 'ccaddress@company.com'}
    ])
print r.status_code
# 200
```

### Optional BCC
The `bcc` kwarg expects a list of dictionaries, where `address` is required
and `name` is optional

```python
r = api.send(
    email_id='YOUR-EMAIL-ID',
    recipient={ 'name': 'Matt',
                'address': 'us@sendwithus.com'},
    email_data={ 'first_name': 'Matt' },
    bcc=[
        {'name': 'BCC Name', 'address': 'bccaddress@company.com'},
        {'name': 'BCC 2 Name', 'address': 'bccaddress@company.com'}
    ])
print r.status_code
# 200
```

### Every possible argument

```python
r = api.send(
    email_id='YOUR-EMAIL-ID',
    recipient={ 'name': 'Matt',
                'address': 'us@sendwithus.com'},
    email_data={ 'first_name': 'Matt' },
    sender={ 'name': 'Company',
                'address':'company@company.com',
                'reply_to':'info@company.com'},
    cc=[
        {'name': 'CC Name', 'address': 'ccaddress@company.com'},
        {'name': 'CC 2 Name', 'address': 'ccaddress@company.com'}
    ],
    bcc=[
        {'name': 'BCC Name', 'address': 'bccaddress@company.com'}
    ])
print r.status_code
# 200
```

## expected response

### Success
	>>> r.status_code
	200

	>>> r.json().get('success')
	True

	>>> r.json().get('status')
	u'OK'

	>>> r.json().get('receipt_id')
	u'numeric-receipt-id'

### Error cases
* malformed request
	
		>>> r.status_code
		400

* bad api key

		>>> r.status_code    
	    403

* email_id not found

	    >>> r.status_code
	    404

### packaging (internal)
        python setup.py sdist upload

