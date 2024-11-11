# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC
## DATE:28.10.2024
## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```
import hmac
import hashlib

def generate_mac(message, secret_key):

    mac = hmac.new(secret_key.encode(), message.encode(), hashlib.sha256)
    return mac.hexdigest()

def verify_mac(message, secret_key, received_mac):

    generated_mac = generate_mac(message, secret_key)
    if hmac.compare_digest(generated_mac, received_mac):
        return True
    else:
        return False

def main():

    message = input("Enter the message: ")
    secret_key = input("Enter the secret key: ")
    
    mac = generate_mac(message, secret_key)
    print(f"Generated MAC: {mac}")
    
    received_message = message
    received_mac = mac  
    
    if verify_mac(received_message, secret_key, received_mac):
        print("MAC is valid. The message is authentic and has not been altered.")
    else:
        print("MAC verification failed. The message may have been altered or is not authentic.")

main()

```
## Output:
![image](https://github.com/user-attachments/assets/b1ac2e83-d7de-4493-95f2-5daa02a1d445)


## Result:
The program is executed successfully.
