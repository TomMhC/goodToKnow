## Data Protection API

### Usage

Encrypts a secret specific to the machine and user that encrypts it given a secret string and an entropy value.

### Reference

`<PackageReference Include="System.Security.Cryptography.ProtectedData" Version="6.0.0" />`

### Encryption

`using System.Security.Cryptography;`

```csharp
var secret = "someSecret";
var entropy = RandomNumberGenerator.GetBytes(16);
var buffer = System.Text.Encoding.UTF8.GetBytes(secret);
var encr = ProtectData.Protect(buffer, entropy, DataProtectionScope.CurrentUser);
Console.WriteLine($"Entropy: '{Convert.ToBase64String(entropy)}'");
Console.WriteLine($"Result: '{Convert.ToBase64String(encr)}'");
```

### Decryption

`using System.Security.Cryptography;`

```csharp
byte[] entropy = Convert.FromBase64String(entropy);
byte[] encr = Convert.FromBase64String(encryptedString);
var decr = ProtectData.Unprotect(encr, entropy, DataProtectionScope.CurrentUser);
Console.WriteLine($"Result: '{Convert.ToBase64String(decr)}'");
```
