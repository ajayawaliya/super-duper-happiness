# super-duper-happiness

from cryptography.fernet import Fernet

# Simulating 3 relay keys
k1 = Fernet(Fernet.generate_key())
k2 = Fernet(Fernet.generate_key())
k3 = Fernet(Fernet.generate_key())

message = b"Hello Tor"

# Client encrypts in reverse order
layer3 = k3.encrypt(message)
layer2 = k2.encrypt(layer3)
layer1 = k1.encrypt(layer2)

# Each relay peels one layer
step1 = k1.decrypt(layer1)
step2 = k2.decrypt(step1)
final = k3.decrypt(step2)

print(final)
