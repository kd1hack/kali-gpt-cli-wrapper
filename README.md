# Kali-GPT-like CLI Assistant

This is a lightweight command-line assistant that simulates a **Kali-GPT-like experience**, designed for security professionals and enthusiasts who work from the terminal.

The tool leverages OpenAI's GPT-4 model and uses a customizable **"Kali" persona** to respond to prompts as if you're interacting with a seasoned cybersecurity assistant.

> 🧠 You can adjust the assistant's persona, tone, or scope to suit your needs — whether for red teaming, blue teaming, or educational purposes.

It’s built for use on **Kali Linux** and other Debian-based systems, packaged as a `.deb` installer for easy distribution and testing.

> 🔑 **Important:** You will need to provide your own OpenAI API key to use this tool. The key is not included or embedded in the script. The assistant integrates with your terminal by reading the `OPENAI_API_KEY` environment variable.

## 📦 Requirements

- Python 3.9 or higher
- OpenAI Python library version 1.0.0 or later  
  You can install it with:

  ```bash
  pip install --upgrade openai
  ```

- A valid OpenAI API key  
  You must export your API key as an environment variable (`OPENAI_API_KEY`) for the tool to function.

## 🚀 Installation

Download and install the `.deb` file using the following commands:

```bash
wget https://github.com/yourusername/kali-gpt/releases/latest/download/kali-gpt-installer.deb
sudo dpkg -i kali-gpt-installer.deb
```

If the installation reports missing dependencies, run:

```bash
sudo apt --fix-broken install
sudo dpkg -i kali-gpt-installer.deb
```

## 🔐 API Key Setup

The CLI tool reads your OpenAI API key from the `OPENAI_API_KEY` environment variable. You can set it temporarily or permanently:

### 🔹 Temporary (session only)

```bash
export OPENAI_API_KEY="your-api-key-here"
```

### 🔹 Permanent (recommended)

To make it persist across terminal sessions, add it to your shell config file:

```bash
echo 'export OPENAI_API_KEY="your-api-key-here"' >> ~/.bashrc
source ~/.bashrc
```

> If you use Zsh, replace `~/.bashrc` with `~/.zshrc`.

## 💬 Usage

Once installed and your API key is set, you can prompt the Kali-GPT-like assistant using:

```bash
kali-gpt "What are some useful Nmap scripts for service detection?"
```

You can ask it anything you'd typically search for — from recon commands to vulnerability explanations — and receive concise answers directly in your terminal.

### 📄 Example: Analyzing Nmap Output via Terminal

You can pipe Nmap results into the assistant using command substitution. For example:

```bash
kali-gpt "Can you analyze this Nmap output and explain what services are exposed? $(cat scan.txt)"
```

Or run a scan and analyze it on the fly:

```bash
kali-gpt "Review this quick scan and suggest next steps: $(nmap -T4 -F 10.0.0.1)"
```

> 💡 Keep outputs short to stay within token limits. For larger scans, trim results or summarize manually.

## 🛠️ Customization

The default assistant uses a Kali Linux–themed persona, but you can customize its behavior by editing the script at:

```bash
/usr/local/bin/kali-gpt
```

### 🔹 Change the model

By default, the assistant uses OpenAI's `gpt-4` model. If you’d prefer a faster and more cost-effective alternative (like `gpt-3.5-turbo`), follow these steps:

#### 📍 Step-by-step:

1. Open the script in a text editor:
   ```bash
   sudo nano /usr/local/bin/kali-gpt
   ```

2. Look for the following line near the top of the file:
   ```python
   model = "gpt-4"
   ```

3. Change it to:
   ```python
   model = "gpt-3.5-turbo"
   ```

4. Save and exit:
   - In nano: press `Ctrl + O` → `Enter` → `Ctrl + X`

5. Test the change:
   ```bash
   kali-gpt "What is the difference between TCP and UDP?"
   ```

> 💡 `gpt-3.5-turbo` is faster and cheaper but may not be as accurate as `gpt-4`.

You can also experiment with future models (e.g. `gpt-4o`) by updating the model name, depending on what your OpenAI API key supports.

### 🔹 Customize the persona

To give the assistant a different tone or expertise (e.g., blue team analyst, malware reverse engineer, or ethical hacker), add a **system message** at the beginning of the message list in the script:

```python
messages = [
    {"role": "system", "content": "You are a professional red team operator helping with command-line and tool advice."},
    {"role": "user", "content": prompt}
]
```

Save the file after editing, and your assistant will behave accordingly.
