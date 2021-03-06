cckeytools
==========

#### Project donation address:

17iwsGKeQfauvLFhTLJjHVEQCDFhiPG3LU

#### Brain Wallet Warning:

It is very dangerous to use a human generated passphrase for a brain wallet.
Use either a cryptographically secure computer generated passphrase or a dice/coin generated passphrase such as diceware.

The passphrase must also be of sufficient length to prevent brute forcing. For cckeygen use 9 to 12 words with the default settings. 


#### Recommended use of this software for secure brain wallets:

First run passgen with 9 to 12 words per passphrase, the default of 10 words is used below:

    ./passgen

Select the passphrase that you find easiest to remember. In most cases it is a good idea to write down this passphrase.

Next run cckeygen with the default settings and use the passphrase you selected in the previous step with a universally unique salt, such as your email address.

For a bitcoin address and private key:

    ./cckeygen -prv

For an electrum wallet seed:

    ./cckeygen --electrum


cckeygen
--------

cckeygen generates cryptographically secure random numbers from a salt and a passphrase using PBKDF2.
This output can be used for Bitcoin private keys and wallet seeds.

#### cckeygen features:

 * Double checks output.
 * Uses three different standard hash algorithms.
 * Outputs private keys, public keys, Bitcoin addresses, armory and electrum wallet seeds, gpg keys, and kdf generated bytes or  * hex characters.
 * Default, fast, and arbitrary iteration settings.
 * Quick self tests performed at every run.

#### Examples:

To run with the default secure settings (SHA-512, 2^20 iterations):

    ./cckeygen.py

To run with the faster settings and output the private and public keys:

    ./cckeygen.py -f -prv -pub

To run with the 25000 iterations (be sure to record how many iterations you use, not recommended for general use):

    ./cckeygen.py -i 25000

To generate and import a gpg private/public key:

    ./cckeygen.py -f --gpg -o key.pem
    cat key.pem | pem2openpgp "User <email@addr>" | gpg --allow-secret-key-import --import
    shred key.pem

passgen
-------

passgen generates cryptographically secure random passphrases from the the operating systems secure random number generator and with additional entropy provided directly by the user.

#### Examples:

To run with the default settings:

    ./passgen.py

To run without the additional user supplied entropy (less secure, relies entirely on the OS RNG):

    ./passgen.py -sue

To run with 12 word passphrases:

    ./passgen.py -w 12
