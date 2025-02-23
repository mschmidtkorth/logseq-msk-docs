- You are able to encrypt your notes at rest i.e. on your hard disk.
- **USAGE**
	- Logseq native encryption
		- _[[Settings]] > Enable encryption feature_ - once you restart, you can set your encryption key
		- Whenever you modify a file it is stored encrypted (on-the-fly).
			-
			  #+BEGIN_TIP
			  Encryption only works for files modified _after_ you enabled it. If you want to encrypt all files, you may use the [logseq-encrypt-ui](https://github.com/kanru/logseq-encrypt-ui) utility. 
			  #+END_TIP
	- [logseq-encrypt-ui](https://github.com/kanru/logseq-encrypt-ui) utility
		- Download as [source](https://github.com/kanru/logseq-encrypt-ui/releases/tag/0.4.0)
		- `brew install rust`
		- `cargo clippy`
		- `cargo build --release`
		- Then check the `/target` folder to execue
		- You need to encrypt/decrypt manually.
	-
	  #+BEGIN_TIP
	  logseq-encrypt-ui can also be used to decrypt all of your files (required to change your encryption key). In addition it will create a plaintext backup copy for you to store in a safe location (`.md.bak`) - make sure to exclude it from your repository. 
	  #+END_TIP
	-
	  #+BEGIN_WARNING
	  * Only text is encrypted, not files or images. 
	  * No unencrypted backup of your data is kept.
	  * You cannot use `git diff` or `git history` for encrypted files.
	  #+END_WARNING