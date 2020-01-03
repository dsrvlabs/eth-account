# eth-account for celo


If you want use Web3.py in your test code,
please clone this repostory & run build.sh to build & install
after that, you can use web3.eth.account.signTransaction, web3.eth.sendRawTransaction

here is my sample code

==================================================
from web3 import Web3, HTTPProvider

FROM_ADDR = ""
TO_ADDR = ""
rpc_url = ""
w3 = Web3(HTTPProvider(rpc_url))
transaction = {
        'to' : TO_ADDR,
        'from' : FROM_ADDR,
        'value' : w3.toWei('0.001','ether'),
        'gas' : 21000,
        'gasPrice' : w3.toWei(20,'gwei'),
        'chainId':121119,
        'nonce': w3.eth.getTransactionCount(FROM_ADDR),
        'feeCurrency' : None,
        'gatewayFeeRecipient' : None,
        'gatewayFee' : 0
        }
with open('keystore file path') as keyfile:
    encrypted_key = keyfile.read()
    private_key = w3.eth.account.decrypt(encrypted_key,'passwd')
    signed_tx = w3.eth.account.signTransaction(transaction, private_key)
    print(signed_tx)
    tx_hash = w3.eth.sendRawTransaction(signed_tx.rawTransaction)
    print(tx_hash)

==================================================
