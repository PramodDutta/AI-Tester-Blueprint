# Google Antigravity Tutorial: 11 Things You NEED to Know

## VIDEO SCRIPT

---

### [INTRO - 0:00-0:45]

**[On screen: Exciting tech intro with Google Antigravity logo]**

Hey everyone! Welcome back to the channel. Today we're diving deep into Google Antigravity - Google's revolutionary new AI-powered IDE that's completely changing how we write code.

If you've been hearing the buzz about Antigravity but aren't sure where to start, you're in the right place. I'm going to walk you through 11 essential things you need to know to master this tool.

By the end of this video, you'll understand exactly what Antigravity is, how to set it up, and how to use its most powerful features to build apps faster than ever before.

Let's get into it!

**[TRANSITION]**

---

### [THING #1: WHAT IS GOOGLE ANTIGRAVITY? - 0:45-2:30]

**[On screen: "1. What Is Google Antigravity?"]**

Alright, let's start with the basics. What exactly IS Google Antigravity?

Google Antigravity is an AI-powered integrated development environment - or IDE - that was released alongside Gemini 3 in November 2025. But here's what makes it different from everything else out there...

Unlike traditional coding assistants that just autocomplete your lines of code, Antigravity is what Google calls an "agent-first" platform. This means the AI doesn't just help you write code - it can actually PLAN entire projects, WRITE code across multiple files, TEST your applications, and even DEBUG issues automatically.

Think of it this way: with tools like GitHub Copilot, YOU'RE still the driver. With Antigravity, you become the ARCHITECT - you tell the AI what to build, and it handles the construction.

The name "Antigravity" itself is pretty clever. In traditional development, there's a lot of "gravity" - the heavy, tedious weight of setting up environments, debugging boilerplate, jumping between terminal, browser, and editor. Antigravity is designed to provide "liftoff" from all of that.

And the best part? It's completely FREE during the public preview, with generous rate limits on Gemini 3 Pro usage.

**[TRANSITION]**

---

### [THING #2: THE THREE SURFACES - 2:30-4:30]

**[On screen: "2. The Three Surfaces"]**

Now let's talk about how Antigravity is organized. The platform operates across three main integrated surfaces, and understanding these is KEY to using the tool effectively.

**First, you have the Agent Manager.**

This is your mission control. Think of it like an inbox where you manage and create AI agents across all your projects. You can spin up new tasks, check progress on running agents, and review completed work - all from this single dashboard. What's really cool is you can have MULTIPLE agents working in parallel, each on different tasks.

**Second, there's the Editor.**

This is the traditional code editor environment - and if you've used VS Code before, you'll feel right at home. You can enter the editor anytime by pressing Command+E or clicking "Open in Editor." It has all the features you'd expect: tab autocomplete, syntax highlighting, and an agent sidebar for AI assistance.

**Third, we have the Browser.**

This is a game-changer. Antigravity has a dedicated browser offering that incorporates the agent directly. You can ask questions like "Test my feature" and the agent will literally spawn a browser, click buttons, scroll, and interact with your app just like a real user would. It can even record videos of these test sessions!

The magic happens when all three surfaces work together seamlessly.

**[TRANSITION]**

---

### [THING #3: INSTALLATION & SETUP - 4:30-6:30]

**[On screen: "3. Installation & Setup"]**

Let's get you set up! Here's how to install Antigravity step by step.

First, head to antigravity.google/download and select the installer for your operating system. It's available for Windows, Mac, and Linux.

**[Show download page on screen]**

For Windows and Mac, it's straightforward - just download and run the installer like any other application.

For Linux users on Ubuntu, you'll need to run a few terminal commands to add the repository and install the package. I'll put the exact commands in the description below.

Once you launch Antigravity for the first time, you'll go through an onboarding process:

1. **Choose your setup flow** - You can import settings from VS Code or Cursor, or start fresh
2. **Pick your theme** - Light or dark mode, your choice
3. **Sign in with your Google account** - You'll need a personal Gmail account for the preview
4. **Configure your Agent Manager settings** - This is the important part!

For the Agent Manager, you'll see different development modes:
- **Agent-driven development** - Full autopilot, the AI does everything
- **Review-driven development** - The AI asks permission for almost every action
- **Agent-assisted development** - This is the RECOMMENDED option. You stay in control, but the AI helps with safe automations

I suggest starting with Agent-assisted development until you get comfortable with how Antigravity works.

**[TRANSITION]**

---

### [THING #4: THE BROWSER EXTENSION - 6:30-8:00]

**[On screen: "4. The Browser Extension - The Secret Weapon"]**

Okay, THIS is what I call the "money feature" of Antigravity - the browser extension.

The Antigravity browser extension allows the AI agent to actually CONTROL your Chrome browser. It can:
- Click buttons
- Fill out forms
- Scroll through pages
- Take screenshots
- Record videos of test sessions

Why does this matter? Because the agent can now TEST your web applications autonomously. When you build a feature, you can tell the agent "Test this" and watch as it opens the browser - indicated by a blue border around the window - and interacts with your app just like a human would.

To set it up:
1. Start a conversation in Antigravity
2. Ask the agent to visit a website
3. It will prompt you to install the browser extension
4. Follow the installation steps in Chrome

Once installed, a browser subagent handles all browser interactions. This subagent can read pages through DOM capture, screenshots, or markdown parsing - and it records everything so you can review later.

This feature alone is what sets Antigravity apart from every other AI coding tool out there.

**[TRANSITION]**

---

### [THING #5: ARTIFACTS - THE TRUST SYSTEM - 8:00-9:45]

**[On screen: "5. Artifacts - Building Trust"]**

One of the biggest questions with AI agents is: "How do I know what it actually did?"

Antigravity solves this with something called **Artifacts**.

Artifacts are markdown files that the agent creates to track its progress, document research, and show you exactly what it accomplished. They appear in the right sidebar in both the Editor and Agent Manager views.

There are three main types of artifacts:

**1. Task List**
This tracks the agent's progress through a project. You can follow along as it completes each item.

**2. Implementation Plan**
Before the agent makes ANY changes to your codebase, it creates this plan. It specs out what it's going to do, what technologies it'll use, and how it'll structure things. You review and approve this BEFORE it starts coding.

**3. Walkthrough**
This comes at the end of a task. It shows exactly what the agent did, including verification steps like screenshots, terminal commands it ran, unit tests it created, or even a full video recording.

This artifact system is HUGE for building trust. You're not just blindly accepting AI-generated code - you can see the entire thought process and verify every step.

**[TRANSITION]**

---

### [THING #6: PLANNING MODE VS FAST MODE - 9:45-11:15]

**[On screen: "6. Planning Mode vs Fast Mode"]**

Antigravity gives you two different modes for working with agents, and knowing when to use each one will make you way more productive.

**Planning Mode**

Use this for complex tasks, deep research, and collaborative work. In Planning Mode, the agent:
- Creates an implementation plan BEFORE writing any code
- Generates a detailed task list
- Waits for your approval at key checkpoints
- Documents everything in artifacts

This is perfect when you're building something substantial or want to stay closely involved in the process.

**Fast Mode**

Use this for simple tasks that need quick execution. In Fast Mode, the agent:
- Executes instructions immediately
- Skips the detailed planning phase
- Gets things done faster

This is great for quick fixes, simple modifications, or when you already know exactly what you want.

You can switch between modes in the agent side panel. My recommendation? Start with Planning Mode for new projects, then switch to Fast Mode once you're familiar with the codebase and just need quick changes.

**[TRANSITION]**

---

### [THING #7: BUILDING YOUR FIRST APP - 11:15-13:30]

**[On screen: "7. Building Your First App"]**

Alright, let's build something! I'm going to show you how to create a simple Pomodoro Timer app using Antigravity.

**Step 1: Create a Workspace**

In the Agent Manager, click "Add Workspace" and select "Open Folder." Create a new folder called "pomodoro-timer."

**Step 2: Write Your Prompt**

In the chat panel, type something like:

"Create a Pomodoro timer web application with: a large visual timer display, focus sessions of 25 minutes, short breaks of 5 minutes, start, pause, and reset buttons, and a clean modern design using HTML, CSS, and JavaScript."

**Step 3: Review the Plan**

The agent will generate an implementation plan showing you exactly what files it's going to create and how it'll structure the app. Take a moment to review this - if something looks off, you can provide feedback before it starts.

**Step 4: Watch It Build**

Once you approve, watch as the agent creates your files, writes the code, and sets everything up. You can see the files appearing in real-time.

**Step 5: Test It**

The agent will launch the app in the browser preview. You can see your Pomodoro timer working! If something isn't quite right, just tell the agent: "The timer text is too small" or "Add a sound when the timer ends" and it'll iterate.

**Step 6: Iterate**

This is the real power of Antigravity. You can keep refining:
- "Add custom input fields for session duration"
- "Make the design more colorful"
- "Add a progress ring around the timer"

Each request, the agent handles automatically.

**[TRANSITION]**

---

### [THING #8: RULES & WORKFLOWS - 13:30-15:15]

**[On screen: "8. Rules & Workflows - Customization Power"]**

As you use Antigravity more, you'll want to customize how the agent behaves. This is where Rules and Workflows come in.

**Rules**

Rules are passive constraints that are ALWAYS active. They're injected into the agent's context to govern its behavior. Use rules for things like:
- "Always use TypeScript strict mode"
- "Never commit secrets to the repository"
- "Use snake_case for Python variables"

Rules restrict HOW the agent does things. They're your guardrails.

**Workflows**

Workflows are active, user-triggered sequences. Think of them like macros. You can create a workflow called "/test" that runs your entire test suite, or "/deploy" that handles deployment steps.

To access these, go to Editor view and look for "Antigravity Settings" at the bottom right. Click on Customizations → Manage to see your Rules and Workflows.

Here's a pro tip: Create a rule early on that enforces your coding standards. Something like "Always add JSDoc comments to functions" or "Use consistent error handling patterns." The agent will follow these automatically in everything it builds.

**[TRANSITION]**

---

### [THING #9: SKILLS - EXTENDING CAPABILITIES - 15:15-17:00]

**[On screen: "9. Skills - Teaching Your Agent New Tricks"]**

Skills are one of Antigravity's most powerful features for customization.

A Skill is a directory-based package containing instructions that the agent can follow for specific tasks. Unlike Rules which are always on, Skills are loaded on-demand when relevant to your request.

Each Skill has:
- A **SKILL.md** file with instructions
- Optional **scripts** the agent can execute
- Optional **references** for context
- Optional **examples** for few-shot learning

For example, you could create a "database-migration" skill that teaches the agent your specific migration process, safety checks, and rollback procedures.

Skills can be stored in two places:
- **Global** (~/.gemini/antigravity/skills/) - Available across all projects
- **Workspace** (.agent/skills/) - Specific to one project

The beauty of Skills is they turn the generalist Gemini model into a SPECIALIST for YOUR project. Instead of repeatedly telling the agent "remember to add the license header" or "follow our commit format," it just knows.

Check out the Antigravity documentation for example Skills you can start with.

**[TRANSITION]**

---

### [THING #10: SECURITY CONSIDERATIONS - 17:00-18:30]

**[On screen: "10. Security - What You NEED to Know"]**

This is important. Giving an AI agent access to your terminal and browser is powerful, but it comes with security considerations.

**Terminal Command Auto Execution**

Antigravity has three policies:
- **Review** - You approve every command (safest, but slowest)
- **Auto** - Common commands run automatically, risky ones ask permission
- **Turbo** - Almost everything runs automatically (fastest, but riskiest)

**Allow Lists and Deny Lists**

You can create lists of commands that are always allowed or always blocked. For example:
- Allow: npm install, git status, python --version
- Deny: curl (prevents data exfiltration), rm -rf (prevents accidental deletion)

**Best Practices:**
1. Start with Review mode until you trust the agent
2. Use a dedicated Google account if possible
3. Never store API keys or secrets in files the agent can access
4. Audit what commands ran in the artifacts
5. Be careful with browser permissions - the agent CAN see and interact with authenticated sessions

Security is YOUR responsibility. The agent is powerful, but treat it like giving a junior developer access to your systems.

**[TRANSITION]**

---

### [THING #11: TIPS FOR SUCCESS - 18:30-20:00]

**[On screen: "11. Pro Tips for Success"]**

Let me wrap up with my top tips for getting the most out of Antigravity:

**1. Write Clear, Goal-Based Prompts**
Don't give step-by-step instructions. Tell the agent WHAT you want to achieve, not HOW to do it. Let it figure out the implementation.

**2. Review Plans Before Approving**
Take the extra 30 seconds to read through implementation plans. Catching issues early saves hours of debugging later.

**3. Use Workspaces Wisely**
Create separate folders for different projects. Don't mix unrelated tasks in a single workspace.

**4. Leverage Parallel Agents**
You can have multiple agents working simultaneously! One researching APIs, another building your frontend, another writing tests.

**5. Learn Git**
Even with AI, version control is essential. If an agent makes changes you don't like, you can always revert.

**6. Iterate, Don't Restart**
If something isn't perfect, tell the agent to fix it. Don't start over - build on what's already there.

**7. Use the Browser Extension**
Seriously, install it. The ability for the agent to test your app automatically is a game-changer.

**8. Provide Feedback in Artifacts**
You can leave comments directly in artifacts, and the agent will incorporate your feedback.

**[TRANSITION]**

---

### [OUTRO - 20:00-21:00]

**[On screen: Subscribe button, like button]**

And there you have it - 11 things you need to know about Google Antigravity!

We covered:
1. What Antigravity is
2. The three surfaces
3. Installation and setup
4. The browser extension
5. Artifacts and trust
6. Planning vs Fast mode
7. Building your first app
8. Rules and Workflows
9. Skills
10. Security considerations
11. Pro tips for success

Antigravity represents a real shift in how we build software. It's not just another AI coding assistant - it's a platform where you stop being the typist and start being the architect.

Download it at antigravity.google/download and give it a try. It's free, and I think you'll be amazed at what you can build.

If this video helped you, smash that like button and subscribe for more tutorials. Drop a comment below telling me what you want to build with Antigravity!

I'll see you in the next one. Peace!

**[END SCREEN with subscribe button and related videos]**

---

## VIDEO DETAILS

**Title Options:**
- Google Antigravity Tutorial: 11 Things You NEED to Know in 2026
- Master Google Antigravity: Complete Beginner's Guide (11 Essential Tips)
- Google Antigravity Explained: The AI Coding Revolution (Full Tutorial)

**Description:**
Learn everything you need to know about Google Antigravity, the revolutionary AI-powered IDE from Google! In this comprehensive tutorial, I cover 11 essential topics including installation, the three surfaces (Agent Manager, Editor, Browser), artifacts, Planning vs Fast mode, Rules & Workflows, Skills, security best practices, and pro tips for success.

🔗 LINKS:
- Download Antigravity: https://antigravity.google/download
- Official Documentation: https://antigravity.google/docs
- Google Codelabs Tutorial: https://codelabs.developers.google.com/getting-started-google-antigravity

⏱️ TIMESTAMPS:
0:00 - Intro
0:45 - #1: What Is Google Antigravity?
2:30 - #2: The Three Surfaces
4:30 - #3: Installation & Setup
6:30 - #4: The Browser Extension
8:00 - #5: Artifacts - Building Trust
9:45 - #6: Planning Mode vs Fast Mode
11:15 - #7: Building Your First App
13:30 - #8: Rules & Workflows
15:15 - #9: Skills
17:00 - #10: Security Considerations
18:30 - #11: Pro Tips for Success
20:00 - Outro

**Tags:**
google antigravity, antigravity tutorial, antigravity ide, gemini 3, ai coding, vibe coding, google ai, antigravity for beginners, how to use antigravity, antigravity tips, agent first development, ai programming, cursor alternative, windsurf alternative, 2026 coding tools

**Estimated Video Length:** 20-21 minutes
