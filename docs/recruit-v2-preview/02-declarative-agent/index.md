---
prev:
  text: Introduction to agents
  link: /recruit-v2-preview/01-introduction-to-agents
next:
  text: Copilot Studio fundamentals
  link: /recruit-v2-preview/03-copilot-studio-fundamentals
short-description: Build and deploy a declarative agent in Microsoft 365 Copilot using Agent Builder
difficulty: 1
codename: OPERATION AGENT DECLARE
time: 45
tags:
  - declarative-agents
products: [microsoft-365, copilot]
industries:
  - it
created-date: 2026-06-28
last-edited-date: 2026-06-28
---

# 🚨 Mission 02: Build a Declarative Agent {#mission-02-declarative-agents}

<mission-meta />

## 🎯 Mission Brief {#mission-brief}

Welcome back, Agent. This mission puts you in the command seat of the fastest way to ship an agent: building one with natural language right where your users already work in **Microsoft 365 Copilot**.

Microsoft 365 Copilot is powerful, but it answers everything. A **declarative agent** makes it answer what matters to your scenario. You define the instructions, knowledge, and starter prompts. Copilot's orchestrator handles the rest. No custom model. No orchestration code. Just a focused agent you can describe, test, and deploy in minutes.

Your weapon of choice? Natural language. Your mission? Design, test, and deploy an IT Help Desk assistant that answers questions using internal and external knowledge sources, all inside Copilot.

In the next missions, you'll first learn Copilot Studio fundamentals, then copy this agent into Copilot Studio and update it for your scenario. Let's get started.

## 🔎 Objectives {#objectives}

In this mission, you'll learn:

1. What a **declarative agent** is
1. How to create an agent in Microsoft 365 Copilot using **Agent Builder**
1. How to describe an agent in natural language and let AI draft the instructions
1. How to ground the agent with document and website knowledge sources
1. How to test and deploy the agent so others can use it

## 🤔 What is a declarative agent? {#what-is-a-declarative-agent}

A **declarative agent** runs on the existing Microsoft 365 Copilot infrastructure using the same large language model and orchestrator that Microsoft 365 Copilot uses and you simply *declare* how it should behave. You provide:

- **Instructions** - the agent's purpose, tone, and rules.
- **Knowledge** - websites, files, or SharePoint sources it can reference.
- **Starter prompts** - example questions to get users going.

You don't manage a model, orchestration, or hosting. That makes declarative agents the quickest way to put a focused assistant in front of users in the Microsoft 365 ecosystem.

> [!TIP]
> When you outgrow a declarative agent and need custom tools, skills, multi-agent orchestration, or your own model, you graduate to a **custom engine agent** in Copilot Studio. You'll build toward that in **Mission 03: Copilot Studio Fundamentals**, then in **Mission 04: Creating a Solution for Your Agent** you'll copy this agent and update it in Copilot Studio.

## 🧪 Lab 02: Build a declarative agent in Microsoft 365 Copilot {#lab-02-build-a-declarative-agent}

### ✨ Use case {#use-case}

As an employee, you want an IT helpdesk assistant that can help you solve common support issues by combining company guidance with trusted web knowledge, so you can troubleshoot faster and get back to work.

### ✨ Prerequisites {#prerequisites}

- A Microsoft 365 Copilot license
- Access to [Microsoft 365 Copilot](https://m365.cloud.microsoft/chat)

### 2.1 Open Agent Builder

1. Go to [Microsoft 365 Copilot](https://m365.cloud.microsoft/chat) and sign in.

1. In the left navigation, under **Agents** 1️⃣, select **New agent** 2️⃣. This opens **Agent Builder**.

    ![Select New agent](./assets/step-01-annotated.png)

### 2.2 Describe your agent in natural language

1. In the message box shown below, copy and enter the natural language prompt given here:

    ```text
    You are an IT Help Desk assistant that helps employees resolve common IT issues and find available devices. Be polite, concise, and helpful. Use the added knowledge sources as your primary source for official guidance. Ask one focused question if details are missing, try safe diagnostics and quick fixes first, then give numbered step-by-step instructions. Do not invent steps. If you cannot verify guidance, say so clearly and recommend safe next steps or escalation. Never ask for passwords.
    ```

    ![Natural language prompt to describe the agent](./assets/step-02-annotated.png)

1. Press **Enter** to submit. Agent Builder drafts your agent by generating a name, description, instructions, and suggested prompts. This takes a few moments.

    > [!WARNING] AI-generated content varies
    > The drafted name, description, instructions, and starter prompts can differ each session.

### 2.3 Name and review your agent

1. The builder switches to the **Configure** view. In the name field shown in the screenshot, replace the suggested name with:

    ```text
    Contoso Helpdesk Agent
    ```

    Review the AI-generated instructions below the name. You'll see the role, tone, and guidance reflected from your description.

    ![Set agent name and review instructions](./assets/step-03-annotated.png)

### 2.4 Add knowledge sources

Next, you'll ground your agent with a guidance document you already have and two website knowledge sources.

#### 2.4.1 Upload guidance document

1. Download your guidance document [Contoso_Guest_WiFi_Connection_Guide.docx](./assets/Contoso_Guest_WiFi_Connection_Guide.docx).
2. In the agent's same **Configure** view, scroll to the **Knowledge** section 1️⃣ and upload 2️⃣ the DOCX guidance document. This gives the agent company-specific information it can use for troubleshooting and device-related questions.

    ![Upload guidance document](./assets/step-02.4.1-annotated.png)

#### 2.4.2 Add website references

1. In the same **Knowledge** section, select the **Enter a URL or name or drop files here** box.

1. Add the first website knowledge source, then press **Enter**:

    ```text
    https://support.microsoft.com
    ```

    ![Add website knowledge source](./assets/step-04-annotated.png)

1. Add the second website knowledge source, then press **Enter**:

    ```text
    https://learn.microsoft.com/troubleshoot
    ```

1. In the same **Knowledge** section, if **Only use specified sources** is available and currently off, turn it on so the agent uses only the knowledge sources you added.

1. When you're done, the **Knowledge** section should show all three knowledge sources.

    - Contoso_Guest_WiFi_Connection_Guide.docx
    - `https://support.microsoft.com`
    - `https://learn.microsoft.com/troubleshoot`

    ![All knowledge sources configured](./assets/step-2.4.2-annotated.png)

### 2.5 Create and deploy the agent

1. Select **Create**. Agent Builder saves the agent and confirms it was created. It's **private** to you by default but you can select **Share** to deploy it to teammates, or **Go to agent** to start using it.

    ![Agent created and deploy options](./assets/step-05-annotated.png)

1. Select **Go to agent**. Your declarative agent opens in Microsoft 365 Copilot, ready for testing.

### 2.6 Test the agent

1. In the message box, enter:

    ```text
    I'm at the Contoso office and can’t get on guest Wi-Fi.
    ```

    ![Agent test prompt](./assets/step-06-annotated.png)

1. The agent responds with numbered, step-by-step instructions grounded in the knowledge you added, using your guidance document for company-specific help and website sources for official supporting information.

    ![Agent test response with document reference](./assets/step-07-annotated.png)

1. Next, test an advanced prompt to validate source scoping and website-only troubleshooting behavior.

1. In the same chat, enter:

    ```text
    I can’t connect to Wi-Fi on my Windows laptop at the office. Please give me a website-based troubleshooting flow only: start with quick checks, then advanced diagnostics, and end with clear escalation criteria. Keep it concise and step-by-step.
    ```

    ![Agent test response with doc and support links](./assets/step-08-annotated.png)


🎉 Congratulations! You built, tested, and deployed a declarative agent entirely inside Microsoft 365 Copilot.

## ✅ Mission Complete {#mission-complete}

You forged a declarative agent that speaks your language, uses trusted knowledge, and runs right inside Copilot. Next up is **Mission 03: Copilot Studio Fundamentals**, where you'll learn the core concepts and interface. Then, in **Mission 04: Creating a Solution for Your Agent**, you'll copy this agent into Copilot Studio and evolve it for your scenario.

⏭️ [Move to the **Copilot Studio Fundamentals** mission](../03-copilot-studio-fundamentals/index.md)

## 📚 Tactical Resources {#tactical-resources}

🔗 [Build agents with Agent Builder](https://learn.microsoft.com/microsoft-365-copilot/extensibility/agent-builder)

🔗 [Declarative agents overview](https://learn.microsoft.com/microsoft-365-copilot/extensibility/overview-declarative-agent)

<analytics-tag section="recruit" mission="02-declarative-agents" />
