"""
Python HMAC:
https://stackoverflow.com/questions/42100488/how-do-i-sign-a-post-request-using-hmac-sha512-and-the-python-requests-library
"""
import hashlib
import hmac
import itertools
import time

import requests


def monotonic_counter():
    """
    Create a monotonic counter seeded with the current time.

    Can store the result as a global variable for generating nonce values.
    """
    return itertools.count(int(time.time() * 1000))


NONCE_COUNTER = monotonic_counter()


def send_hmac_post(hmac_secret, url, data):
    headers = {'Api-Key': '3gy3820af390areuwaf0y32830'}
    payload = {'data': data, 'nonce': next(NONCE_COUNTER)}
    request = requests.Request('POST', url, data=payload, headers=headers)
    prepped = request.prepare()
    signature = hmac.new(hmac_secret, prepped.body, digestmod=hashlib.sha512)
    prepped.headers['HMAC'] = signature.hexdigest()

    response = None
    with requests.Session() as session:
        response = session.send(prepped)
    return response


class RequestBodyHMAC(object):
    default_algorithm = hashlib.sha512

    def __init__(self, hmac_secret, header_name='HMAC', algorithm=None):
        self.header_name = header_name
        self.hmac_secret = hmac_secret
        self.algorithm = algorithm or self.default_algorithm

    def __call__(self, request):
        signature = hmac.new(
            self.hmac_secret, request.body, digestmod=self.algorithm
        )
        request.headers[self.header_name] = signature.hexdigest()


def send_hmac_with_auth(hmac_secret, url, data):
    """This requires adding the nonce to the payload in advance."""
    response = requests.post(
        url, data=payload, headers=headers, auth=RequestBodyHMAC(hmac_secret)
    )
    return response


if __name__ == '__main__':
    payload = {'stuff': 'things'}
    response = send_hmac_post(api_url, payload)
    print(response.status_code)
