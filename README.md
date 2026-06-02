# ⚡ @crypto/aes-gcm — AES-256-GCM Authenticated Encryption for Zeta

**Port of the Rust `aes-gcm` crate (v0.10.x). Pure Zeta implementation of
AES-256 in Galois/Counter Mode per NIST SP 800-38D.**

---

## 📦 Package

```
zorbs add @crypto/aes-gcm
```

## 🔧 API

### Low-level AES-256

```zeta
let cipher = Aes256::new(&key);
let encrypted = cipher.encrypt_block(&block);  // 16-byte block
let decrypted = cipher.decrypt_block(&encrypted);
```

### AES-256-GCM (Recommended)

```zeta
// Encrypt
let (ciphertext, tag) = aead.encrypt(&nonce, plaintext, aad);

// Decrypt (returns empty on auth failure)
let plaintext = aead.decrypt(&nonce, ciphertext, aad, &tag);
```

### Convenience AEAD (ciphertext || tag)

```zeta
let encrypted = aead_encrypt(&key, &nonce, "hello", "aad");
let decrypted = aead_decrypt(&key, &nonce, &encrypted, "aad");
```

### Key Wrap / Unwrap

```zeta
let wrapped = key_wrap(&kek, &key);
let unwrapped = key_unwrap(&kek, &wrapped);
```

## 🔒 Security Properties

- **128-bit security level** (AES-256 provides 256-bit keys with 128-bit post-quantum security)
- **Authenticated encryption**: confidentiality + integrity
- **Nonce reuse is catastrophic**: never reuse a (key, nonce) pair
- **Constant-time tag verification**: prevents timing oracles

## 📦 What's Inside

| Module | Source | Description |
|---|---|---|
| `Aes256` | aes v0.8.x | AES-256 block cipher (14 rounds) |
| `Aes256Gcm` | aes-gcm v0.10.x | GCM mode AEAD |
| `GHash` | ghash v0.5.x | GHASH authentication |
| `aead_encrypt/decrypt` | aead traits | Convenience AEAD API |
| `key_wrap/unwrap` | — | Key wrapping with AES-GCM |

## 📄 License

MIT OR Apache-2.0
