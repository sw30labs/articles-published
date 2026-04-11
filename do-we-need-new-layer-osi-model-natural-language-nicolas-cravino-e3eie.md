![](https://media.licdn.com/mediaD4E12AQHJMfjv0_54kw)

# [Do We Need a New Layer in the OSI Model for Natural Language?](https://www.linkedin.com/pulse/do-we-need-new-layer-osi-model-natural-language-nicolas-cravino-e3eie)

Created on 2024-11-20 18:07

Published on 2024-11-20 18:56

Over the past few years, I’ve had the privilege of working on a variety of generative AI projects, ranging from applications that use **static and dynamic prompts** to more complex systems that leverage **agents, teams of agents, and group chats**. These experiences have given me a front-row seat to the immense power and versatility of AI—but also to its potential vulnerabilities.

One recurring theme I’ve observed is the **security and governance challenges associated with prompts**, especially **dynamic prompting**, where inputs are constructed during execution based on variables and conditions. In environments with **agents interacting in group settings**, the complexity and potential for unintended consequences multiply rapidly.

> This led me to ask a critical question: **Do we need to rethink how we approach prompts and natural language interactions in the broader context of system design? Could the OSI model, which has guided us for decades, benefit from a new layer dedicated to natural language?**

---

## The Case for a Natural Language Layer

### 1. Natural Language’s Unique Challenges

Natural language interactions are fundamentally different from traditional protocols handled in **Layer 7 (Application Layer)**:

* **Ambiguity**: User inputs can be vague or context-dependent.
* **Dynamic Nature**: Prompts are often constructed during runtime, influenced by variables and conditions.
* **Security Risks**: Vulnerabilities such as **prompt injection** and **data leakage** emerge in the absence of standardized governance.

>  Existing layers lack the tools to securely and efficiently handle these complexities, leaving natural language inputs vulnerable to exploitation and mismanagement.

### 2. Responsibilities of the Natural Language Layer

 A dedicated layer would focus on:

* **Interpretation**: Understanding user intent and context.
* **Validation**: Ensuring prompts are safe, ethical, and free from injection vulnerabilities.
* **Mapping**: Translating natural language into structured requests for Layer 7 protocols.
* **Explainability**: Providing transparent and interpretable feedback to users.

By isolating natural language concerns, we ensure modularity, security, and standardization across systems.

![](https://media.licdn.com/dms/image/v2/D5612AQF-59tsCB7F5Q/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1732210477728?e=1776297600&v=beta&t=0otnVrzrmhR1-iIgOmrmx7Y8WdpfFaIASzVr9XtEhnY)

This conceptual layer would handle the natural language input before it is processed as structured data by Layer 7. Enhancing Layer 7 without a separate layer might blur responsibilities, whereas isolating NLP responsibilities in a dedicated layer ensures clarity.

### 3. What Happens Without This Layer?

In its absence, natural language processing (NLP) tasks remain scattered across multiple layers, leading to:

* I**nconsistent Governance**: No centralized framework for handling user inputs securely.
* **Increased Vulnerabilities**: Dynamic prompts expose systems to risks that traditional protocols don’t address.
* **Lack of Standards**: Organizations must create custom solutions, increasing development overhead and interoperability challenges.

### 4. The Alternative: Enhancing Layer 7

If creating a new layer seems excessive, a feasible alternative could be considering enhancing **Layer 7**:

* **Sub-layer for NLP**: A dedicated sub-layer for handling natural language interactions.
* **Standardized APIs**: Universal APIs for prompt validation, intent resolution, and NLP governance.
* **Integrated Security**: Built-in safeguards against misuse and injection attacks.

---

### 5. Pros and Cons in principle

***A. Adding a New OSI Layer***

**Pros:** Clear demarcation of NLP concerns.Facilitates the development of universal standards for natural language interactions. Enhances modularity, allowing developers to build on a standardized foundation.

**Cons:** Significant paradigm shift for existing OSI-based systems. Resistance from industries reluctant to adopt new models.

***B. Enhancing Layer 7***

**Pros:** Less disruptive than introducing a new layer. Easier integration with existing protocols and systems.

**Cons:** Risks conflating diverse concerns within a single layer. May still lack the modularity needed for effective governance.

---

### 6. Challenges and Risks

**Fragmentation Risk:** Without industry consensus, creating a new layer or enhancing Layer 7 could lead to divergent, incompatible implementations.

**Complexity in Design:** A dedicated NLP layer could introduce complexity for developers unfamiliar with natural language processing concerns.

**Ethical Implications:** Addressing the ethical use of NLP frameworks (e.g., ensuring bias-free, equitable interactions) will require interdisciplinary collaboration. Handling natural language at scale introduces complex ethical concerns, including:

* **Bias in Prompt Processing:** Natural language models trained on biased data could propagate stereotypes or misinformation. The layer must include mechanisms to identify and mitigate biases, ensuring fairness in interactions.
* **Privacy and Data Sensitivity:** Dynamic prompts often involve user-specific data. The Natural Language Layer must implement robust encryption and anonymization to prevent leaks or misuse.
* **Transparent Decision-Making:** Users must be able to understand why a certain interpretation or response was generated. Explainability frameworks should allow users to query how their inputs were processed and why specific outputs were provided.

***Practical Ethical Scenario:*** *Imagine a healthcare chatbot designed to assist with patient inquiries. If the NLP system misinterprets user intent due to ambiguous phrasing, it could lead to harmful advice. A Natural Language Layer would validate inputs, check for ambiguities, and flag potentially unsafe queries, ensuring that only validated requests reach Layer 7 for processing.*

---

### 7. Where Do We Draw the Demarcation Line?

One critical challenge is determining **who bears the responsibility for implementing and executing these controls**: the application developer, the LLM provider during test-time (inference) compute ?, both ?.

***A. Should It Be the App Developer?***

Developers integrating NLP into their systems could be responsible for embedding controls such as prompt validation, bias detection, and ethical guardrails. This approach offers flexibility, allowing developers to tailor the Natural Language Layer to their specific needs.

**Advantages:** Customization ensures that the controls align closely with the application's goals and user base. Developers retain direct control over how inputs and outputs are managed.

**Disadvantages:** Places a significant burden on developers, requiring expertise in NLP governance. Leads to inconsistencies across implementations, increasing fragmentation and security risks.

***B. Should Controls Be Built into LLM Test-Time Compute?***

As LLMs continue to evolve, runtime systems could embed governance mechanisms that automatically apply during inference (execution). This approach leverages the power of the model itself to enforce security, validation, and ethical processing. *(we have seen a glimpse of this test-time compute focus with OpenAI o1 Preview, OpenAI is applying chain-of-though at test time compute. Nothing prevent them from applying extra steps too.)*

**Advantages:** Centralized controls improve consistency and reduce the burden on developers. LLM providers can update and refine these mechanisms as models improve.

**Disadvantages:** Potentially shifts too much control to LLM providers, reducing developer autonomy. Could introduce latency or performance trade-offs during runtime processing.

***C. A Hybrid Approach?***

A hybrid model may offer the best balance, with some responsibilities lying with the developer (e.g., application-specific validation) and others embedded in the LLM’s runtime systems (e.g., universal safeguards like bias detection).

This challenge underscores the importance of **establishing clear guidelines and standards** to delineate responsibilities effectively. Without clarity, both developers and LLM providers risk overlooking critical controls, increasing the likelihood of vulnerabilities or ethical lapses.

---

### How This Fits the Broader Case

Addressing the question of responsibility reinforces the need for a centralized Natural Language Layer. By isolating NLP concerns, we can provide a modular framework where controls can be distributed sensibly between developers and runtime systems. As LLMs improve, these responsibilities can shift dynamically, ensuring future-proof systems.

### 8. Looking Forward

As we integrate AI more deeply into our systems, the need for a dedicated framework to handle natural language interactions becomes increasingly clear. Whether through a **Natural Language Layer** or an enhanced Layer 7, we must address:

* How natural language is constructed and processed.How to secure prompts and user inputs dynamically.
* How to ensure ethical and responsible use of natural language interfaces.

I invite the community to join the conversation. Should we expand the OSI model to include a natural language layer, or are incremental enhancements sufficient? Let’s explore how we can prepare the OSI model for the challenges and opportunities of the AI era.

***Note:*** Please do not interpret my idea as a call for additional regulatory oversight. Instead, consider it as a need for less fragmented and more centralized technical guidance.

---

**References and Further Reading**

* [My GitHub Profile](https://github.com/spidernic) – Explore my personal projects and contributions, including generative AI systems and experiments with agent-based interactions.
* My LinkedIn Articles – Read my other insights and thoughts on AI and cutting-edge technologies.

**Community Resources**:

* [https://genai.owasp.org/llm-top-10/](https://owasp.org/www-project-top-10-ai-risks/)– A resource for understanding AI-specific threats, including prompt injection and excessive agency.
* Below is a list of LLMs that it's main purpose is to act as a Natural Language Firewall, giving as an output a 'Pass' or 'Fail' and in some cases the pass/fail ationale behind. Google with *ShieldGemma*, Meta with *LlamaGuard*, and IBM with *GraniteGuardian*, and I can only wait for Microsoft to publish one of similar characteristics.

<https://huggingface.co/google/shieldgemma-27b>

<https://huggingface.co/meta-llama/Llama-Guard-3-1B>

<https://huggingface.co/ibm-granite/granite-guardian-3.0-8b>