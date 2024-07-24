## Secure Note-Taking with WASM Sandboxing

### Introduction

The intent of this mini-project is to build a backend system that demonstrates creating sandboxed environments for running user-submitted code. Our goal is to execute this code in a restricted manner, preventing unrestricted access to the backend while providing controlled access through carefully designed APIs.

This project is inspired by my recent fascination with Smart Contract runtimes in blockchain systems. Blockchains run user-submitted smart contracts in a WebAssembly (WASM) runtime, restricting their access and providing resources only through specific APIs. This mini-project aims to mimic this behavior in a simplified context.

By building a secure note-taking application, we'll explore the principles of sandboxing, API design for restricted environments, and secure execution of untrusted code - all key concepts in blockchain and other secure computing environments.

This project mirrors blockchain environments by having sensitive data (encrypted notes and master key) coexisting with untrusted code (user plugins) on the same system. It will give you hands-on experience with WASM runtimes, sandboxing, and API design for secure execution environments.

### Problem Statement
Create a secure note-taking application that allows users to store encrypted notes and run custom WASM plugins to process note content, while maintaining strict security boundaries between the core system and user-submitted code.

**Simplified User Flow**

Notes Management
1. User creates a Note. The backend encrypts it with a master key and stores it in the DB (or in memory for now).
2. User can edit/delete a Note too. (Editing is not a priority for now.)
3. User can view all their Notes. 


Plugin System Flow
1.  User submits a plugin written in Rust and compiled to wasm to the system. 
2.  Plugin Examples: 
	-  Text summarizer
	- Text Analyzer: Counts words, sentences, and provides readability scores.
	-   Keyword extractor
	-   Code syntax highlighter
3.  User selects a note to use the plugin for and get the result. 


### Core Components:

1.  A main application that stores encrypted notes
2.  A WASM runtime for executing user-defined plugins

### Features:

1.  Note Storage:
    -   Users can create, read, update, and delete encrypted notes
    -   The application holds a master key for encrypting/decrypting notes
2.  Plugin System:
    -   Users can write and upload custom plugins as WASM modules
    -   Plugins can perform operations on note content (e.g., text analysis, formatting)
3.  Sandboxed Execution:
    -   Plugins run in a restricted WASM environment
    -   The runtime should prevent plugins from accessing the master key or raw note data
4. Secure API for Plugins:
	-   Expose a set of controlled APIs to plugin code for interacting with the main application
	-   APIs provide limited, secure access to note content and app functionality
	-   Implement strict input validation and output sanitization for all API calls


### Requirements

The primary aim of this project is to learn about sandboxing in backend systems. To achieve this, the following requirements must be met:

1.  Secure Sandboxing:
    -   Execute plugin code (WASM) in a strictly controlled sandbox environment
    -   Implement robust isolation between the sandbox and the main system
    -   Ensure plugins cannot access or modify system resources outside their allocated sandbox
2.  Controlled API Access:
    -   Design and implement a secure API that exposes only necessary functionalities to plugins
    -   Provide controlled, on-demand access to decrypted note content through the API
    -   Implement strict input validation and output sanitization for all API calls
3.  Data Security:
    -   Prevent plugin code from accessing or inferring the encryption/decryption keys
    -   Implement mechanisms to detect and prevent unauthorized data retention by plugins
    -   Ensure that sensitive data (like decrypted notes) is only held in memory temporarily during plugin execution
4.  Resource Management (Bonus points if you use something like [finite-wasm](https://github.com/near/finite-wasm/tree/main)):
    -   Implement resource limits for plugin execution (e.g., memory usage, CPU time)
    -   Design a system to monitor and control plugin resource consumption
5. Basic Error Handling:
	-   Implement fundamental error handling for plugin execution and API interactions
	-   Add minimal logging for critical operations to aid in debugging and basic security monitoring


### Initial thoughts on next Steps:
1.  Set up the basic Rust project structure
2.  Implement the core note storage and encryption system
3.  Integrate a WASM runtime (e.g., Wasmtime)
4.  Design and implement the plugin API
5.  Create the sandboxed environment for plugin execution
6.  Implement plugin management features. (Something simple)
7.  Develop sample plugins. 
8.  Implement error handling and logging
9.  Conduct security testing and optimizations(bonus). 
