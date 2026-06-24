# Free-Tier Claude on Cursor via AWS Bedrock

Bring your own key (BYOK) performance meets zero out-of-pocket development. This guide walk you through how to claim $100 to $200 in free AWS credits, request access to Anthropic's frontier Claude models on Amazon Bedrock, and safely route them directly into the Cursor IDE. By bypassing expensive personal subscriptions, you unlock the fastest, most reliable frontier-tier AI code generation.

---

## Phase 1: AWS Onboarding & Unlocking the Paid Tier

To access enterprise-ready AI services such as Amazon Bedrock, you must onboard with a verified billing profile.

1. **Sign Up for a Standard AWS Account:**
   * Navigate to the [AWS Registration Page](https://aws.amazon.com/) and create a standard personal account.
   * Provide a valid credit or debit card for identity verification. AWS will process a temporary $1 authorization hold to verify card validity, which is returned in 3-5 business days.

2. **Verify/Upgrade to the Paid (Pay-as-you-go) Plan:**
   * **Crucial Step:** By default, new accounts might experience limitations in provisioning resource quotas or accessing model registries. You must explicitly verify your account is associated with a standard **Pay-As-You-Go** billing plan.
   * Go to the **AWS Billing Console**. Under **Billing Preferences** and **Payment Methods**, ensure your payment profile is fully verified with no outstanding balances.
   * *Note:* Verifying or operating on the Pay-As-You-Go tier **does not** charge you immediately nor does it void your eligible AWS Free Tier benefits. It simply removes the sandbox barriers, allowing you to ingest promotional credits and request model access.

[Insert Screenshot: AWS Billing Console highlighting Payment Methods and Pay-As-You-Go/Verified status]

---

## Phase 2: Claiming $100-$200 in Baseline Onboarding Credits

Before applying for large startup grant programs, stack baseline credits directly from the AWS Console to fully offset your early API usage.

1. **Locate the Credit Widget:**
   * Go to the AWS Console homepage dashboard.
   * Look for the widget titled **Explore AWS / Earn AWS credits** or go directly to the **Billing -> Credits** page.

2. **Complete the 5 Console Onboarding Mini-Tasks:**
   AWS rewards developers with active credits (typically **$20 each**) for completing simple platform interactions:

   * **Task 1: Set up an AWS Budget Alert ($20)**
     * Create a cost budget to monitor your spend (details in Phase 3).
   * **Task 2: Use the Amazon Bedrock Playground ($20)**
     * Launch the Bedrock console, open the Chat or Text Playground, select any model, and send a sample developer prompt.
   * **Task 3: Create an AWS Lambda Function ($20)**
     * Navigate to AWS Lambda, select "Create function" from boilerplate Node.js or Python templates, and test run it once.
   * **Task 4: Spin up and Terminate an EC2 Server ($20)**
     * Launch a single `t2.micro` or `t3.micro` instance using the AWS Free Tier AMI, and then immediately terminate it.
   * **Task 5: Launch a Free-Tier RDS Database ($20)**
     * Instantiate a micro database (e.g., PostgreSQL or MySQL) under the RDS Free Tier configuration, then delete it.

3. **Verify Active Credit Balance:**
   * Navigate to **Billing Console -> Credits** to confirm your active credit voucher stack.
   * Your credits will automatically apply to any downstream Bedrock inference charges before your card is ever billed.

[Insert Screenshot: AWS Credits Console page showing a positive promotional credit balance of active, unexpired vouchers]

---

## Phase 3: Setting Up a Budget Alert & Safeguarding Your Balance

To guarantee that your out-of-pocket setup costs remain strictly $0, establish a hard ceiling via AWS Budgets.

1. Navigate to the **AWS Budgets Console**.
2. Click **Create budget** on the top right.
3. Select the **Cost budget** option (Recommended) and click **Next**.
4. Configure the following parameters:
   * **Period:** Monthly
   * **Budget renewal type:** Recurring budget
   * **Budgeting method:** Fixed
   * **Budget limit:** `5` (Set a strict $5.00 limit)
5. Configure your Threshold Alerts:
   * Click **Add an alert threshold**.
   * Set the threshold at **100%** of the budgeted amount (Alerts at $5 spent) or **80%** (Alerts at $4 spent).
   * Set the **Trigger** type to both **Actual** and **Forecasted** (so you are warned if current trajectories estimate a $5 breach).
6. Configure Email Notifications:
   * Input your primary developer email.
   * (Optional) Connect to an Amazon SNS topic for SMS or webhook triggers.

[Insert Screenshot: AWS Budget creation console showing a $5 cost limit with active actual/forecasted email alerts configured]

---

## Phase 4: Requesting Model Access in the Amazon Bedrock Catalog

To interact with Anthropic's Claude models, you must manually request access with a single-click request.

1. Open the [Amazon Bedrock Console](https://console.aws.amazon.com/bedrock/).
2. Select a target region supporting the flagship Claude models. **US East (N. Virginia)** (`us-east-1`) or **US West (Oregon)** (`us-west-2`) are highly recommended.
3. In the left-hand navigation pane, scroll to the absolute bottom and select **Model access**.
4. In the main window, click the **Manage model access** button in the top right.
5. Locate the **Anthropic** collection and check the specific options for:
   * **Claude 3.5 Sonnet**
   * **Claude 3.5 Haiku**
   * **Claude 4.6 Sonnet** (or latest available Claude models)
6. Click **Save changes** / **Submit**.
7. *Verification:* No long forms or company URLs are required. Access is typically granted automatically within 1 to 5 minutes. Refresh the page to verify the status is marked **Access granted**.

[Insert Screenshot: Amazon Bedrock 'Model access' interface showcasing green checkmarks and 'Access granted' status for the Anthropic Claude product suite]

---

## Phase 5: Understanding Bedrock Quotas & Inference Types

Amazon Bedrock uses three structural routing lanes for querying frontier models. Understanding these is essential for configuring your IDE without hitting request limits:

| Routing Lane | Description | Target Use Case & TPM / RPM Guidelines |
| :--- | :--- | :--- |
| **On-Demand** | Traditional single-region endpoint request mapping. | **Localized region locks.** May experience lower rate ceilings (Transactions Per Minute, or TPM) or outright depletion (e.g., 0 TPM) during peak continent hours. |
| **Geo Cross-Region** | Automatically balances requests over endpoints within the same continent. | **Stable production and regional compliance.** Delivers higher availability and limits local outages by moving traffic seamlessly. |
| **Global Cross-Region** | Dynamically bounces requests globally to the optimal available data center. | **Active development environment.** Uses strings like `us.anthropic.claude-sonnet-4-6` or `us.anthropic.claude-3-5-sonnet` to tap into massive 6M+ TPM thresholds with the lowest latency. |

### Handling "0 TPM" Limits & Requesting Increases
If a newly requested flagship model is limited to 0 TPM or you hit throttling errors, follow these steps:
1. Click the vertical dots `⋮` adjacent to the model in the **Model access** section.
2. Select **Edit quota** or navigate to **AWS Service Quotas**.
3. Submit a modest limit increase request (e.g., set to `50,000` or `100,000` TPM).
4. For verified pay-as-you-go checked accounts, validation and approval are generally resolved within a few hours.

[Insert Screenshot: AWS Bedrock Quotas interface displaying active Transactions Per Minute (TPM) limits for Anthropic model families]

---

## Phase 6: Budget Preservation Strategy (How to avoid draining the $100)

Maximal credit lifespan is achieved by selective, context-aware model calling. Route your tasks to these two primary models:

### 1. Claude 3.5 Haiku (`us.anthropic.claude-3-5-haiku`)
* **Task Type:** Repetitive syntax auditing, standard code generation templates, quick single-file debugging loops.
* **Pricing Efficiency:** The cheapest operational model that easily fits inside minor credit margins. Use this for 80% of daily programming assistance.

### 2. Claude 3.5 / 4.6 Sonnet (`us.anthropic.claude-sonnet-4-6` or `us.anthropic.claude-3-5-sonnet`)
* **Task Type:** Elite multi-file refactoring, systemic architecture planning, heavy math or logic operations.
* **Pricing Efficiency:** The perfect intersection of flagship performance and moderate consumption pricing.

### ⚠️ Crucial Warning Note:
Avoid selecting the **1M Context Length** specialized variants in Cursor for simple, daily coding. Processing extremely large files across massive context windows (over 200K tokens) can incur high input billing fees that quickly deplete your promotional credits. Always keep your codebase context panels curated and clean.

---

## Phase 7: Generating Secure IAM Credentials

To connect Cursor to Bedrock, you must establish secure, scoped API credentials. Never use your main administrative AWS root user credentials.

1. Navigate to the **AWS IAM Console** (Identity and Access Management).
2. In the sidebar, select **Users** and click **Create user**.
3. Configure User Details:
   * **User name:** `cursor-user`
   * **Console access:** *Do not check* "Provide user access to the AWS Management Console" (this is a programmatic-only API user).
4. Set Permissions:
   * Select **Attach policies directly**.
   * Search for and check the box next to **`AmazonBedrockFullAccess`**. (For maximum security, you can alternatively attach a custom policy that only permits `bedrock:InvokeModel` and `bedrock:InvokeModelWithResponseStream` on Anthropic models).
5. Review and click **Create user**.
6. Generate CLI Credentials:
   * Click on the newly created `cursor-user` in the list.
   * Select the **Security credentials** tab.
   * Scroll to the **Access keys** section and click **Create access key**.
   * Select **Command Line Interface (CLI)** or **Other** as the use case.
   * Click through and copy both parameters:
     * **Access Key ID**
     * **Secret Access Key**
   * *Important:* Copy these immediately or download the `.csv` file. Once you close this window, the Secret Access Key cannot be recovered.

[Insert Screenshot: AWS IAM Console displaying successful completion of the Access Key set for 'cursor-user']

---

## Phase 8: Configuring Cursor IDE (Fixing Common Routing Bugs)

Link your secure IAM keys inside the IDE to execute high-speed, local LLM payloads.

1. Launch your **Cursor IDE**.
2. Click the gear icon (**Settings `⚙️`**) in the top right corner (or press `Cmd/Ctrl + Shift + J`).
3. Select **Models** in the settings configuration pane.
4. Scroll down to the **AWS Bedrock** dropdown block and toggle it to **ON**.
5. Input your programmatic AWS parameters:
   * **Access Key ID:** `Your_IAM_Access_Key_ID`
   * **Secret Access Key:** `Your_IAM_Secret_Access_Key`
   * **Region:** Enter the specific geographical code where your models were requested (e.g., `us-east-1` or `us-west-2`).
6. Specify the exact model string by writing it in the test model input:
   * For Global Cross-Region Sonnet: `us.anthropic.claude-sonnet-4-6` or `us.anthropic.claude-3-5-sonnet`
   * For Global Cross-Region Haiku: `us.anthropic.claude-3-5-haiku`

### 🔧 Critical Troubleshooting Alert (Avoiding Code 400 Payload Mangling)
If Cursor throws a request failure:
`Request failed with status code 400: {"message": "model is required"}` or displays an unrecognized endpoint error, it is pointing to a metadata payload collision.

* **The Cause:** Active integrations from other providers (especially **Azure OpenAI** or custom OpenAI endpoints) can sometimes leak their header structures into simultaneous prompt calls, corrupting the requests sent to Bedrock.
* **The Resolution:** Navigate back to the Cursor **Models** settings panel and toggle **OFF (Gray)** all other unused third-party blocks (particularly Azure OpenAI and local LLM override configurations). This ensures your API client builds a clean, standard AWS header payload, instantly resolving the error.

[Insert Screenshot: Cursor IDE Models setting panel with AWS Bedrock active, IAM keys populated, and other conflicting providers switched completely off]
