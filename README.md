# Document Comparison with watsonx Orchestrate AI Agent

![](documents/doc_compare.jpg)

Ever spent hours combing through two nearly identical contracts, just to find that one sneaky clause that changed everything?  

In this hands-on bootcamp, we’ll show you how to let AI do the heavy lifting. Discover how IBM’s watsonx Orchestrate AI Agent can revolutionize document comparison, turning a tedious manual task into a fast and reliable workflow.

## What You’ll Learn

In this session, you’ll:
* Learn how to orchestrate workflows in watsonx Orchestrate using a custom AI Agent and tool.
* Extract document differences through chatting to the agent.
* Discuss the possibility of using additional pre-built agents.


## Use Case: Contract Review Accelerator

Imagine you’re part of a legal team reviewing two versions of a vendor contract:
* Version A from last quarter
* Version B just received today

Instead of manually comparing every clause, your watsonx Orchestrate agent works for you:
1.	Extracts document terms.
2.	Feeds the content to the agent, which applies semantic matching and highlights critical differences (e.g., pricing, liability, renewal terms).
3.	Generates a summary report for immediate review.

In minutes, you’ll know what changed, why it matters, and what to do next.

## watsonx Orchestrate

### Environment setup
To get to the watsonx Orchestrate console, go the [Resources list on the IBM Cloud homepage](https://cloud.ibm.com/resources).

![alt text](documents/image1.png)

Expand the `AI / Machine Learning` section and select the resource that has `watsonx Orchestrate` in the Product column, as shown above. Next, click on the `Launch watsonx Orchestrate` button.

![alt text](documents/image2.png)

This opens the watsonx Orchestrate console.

![alt text](documents/image3.png)

### UI walkthrough

> When opening the console for the very first time, you may be greeted by a pop-up window offering that you create your first agent. Click on `Skip for now`.

![alt text](documents/image4.png)

In the console, it shows that no agents have been deployed yet. Thus, if you interact with watsonx Orchestrate at this point, not much will happen, since the system has no agents available to route any request to.

Go ahead and chat with watsonx Orchestrate to explore what type of answers it gives to your questions.

### Create an agent 
We are now ready to build the first agent. In the watsonx Orchestrate console, click on either `Create or Deploy` or `Create new agent` (either will get you to the same place).

![alt text](documents/image6.png)

However, if you add your document as the knowledge base in agent, it will be able to do tasks like summarization. 
![alt text](documents/image5.png)

#### The Legal Contract Comparison Agent
In the following screen, click on `Create agent`.

![alt text](documents/image7.png)

On the following page, you can select if you want to create the new agent from scratch or from a template, and give it a name and a description.

 Let's start by giving it a name and a description:
- Name: Legal Contract Comparison Agent
- Description: 
```
This agent is used to compare the differences between the legal contract documents provided.
```

Note that in the world of AI Agents, these descriptions are not merely used as documentation, they are also used in making decisions about selecting the right agent for the job, so what you enter into this field is important.

After you have entered the required information, click on `Create`.

<img width="600" alt="image" src="documents/image8.png">

On the following screen, we can enter more information about the new agent we are building. Agents can rely on `Knowledge`, on a `Toolset` that consists of one or more `Tools` and one or more `Agents` to satisfy a request that is sent to them. Moreover, you can pick the `AI Model` that it uses under the covers, as well as the `Agent style` and the `Voice modality`. We can define all of those elements here. 
- `Knowledge` represents information that is stored in the form of "embeddings" in a so-called Vector Store. Whenever the agent answers a request, it can choose to run a search against the connected Knowledge repository (i.e. the Vector Store) to search for information that can assist in answering the request. You can either upload documents directly here, or connect the agent to an already existing repository. Note that once again, the "Description" field is key, because it will help the agent decide whether to run a search against the knowledge.
- The `Toolset` contains other components that the agent can delegate certain tasks to. 
  - `Tools` are functions an agent can call. It can be either an API call or an invocation of custom code. This allows to extend the agent's capabilitiy beyond what the LLM has been trained with.
  - `Agents` are other agents, either within watsonx Orchestrate or running externally, e.g., in watsonx.ai that this agent can delegate the request, or part of a request, to.

Moreover, you can specify the Large Language Model that the agent will use, as well as the "style" of the agent. For this agent, we will pick the `llama-3-405b-instruct` model and keep the `Default` style.

<img width="800" alt="image" src="documents/image9.png">

#### Create Agentic Workflow

We will create an agentic worlkflow and import it as tool to be used by the agent.

Lets go ahead and create an agentic workflow.

<img width="800" alt="image" src="documents/image10.png">

Provide `Name` and `Description` of the workflow. 
- Name: ```document comparison tool```
- Description: 
```
Compare between legal documents
```

<img width="800" alt="image" src="documents/image11.png">



## Credits
<details><summary>IBM Client Engineering Team</summary>

#### Business Technical Leader 
* Vincent Lee

#### Instructors
* Zack Phillips
* Pengxiang Xu
* Kyle Skyllingstad
* Chaithra M. Nagaraj
* Vrisan Dubey

#### AI Engineers
* M N Navneeth
* Tiyasa Mukherjee
* Fidha Haneefa
* Kousalya V

#### Designer
* Amy Luo

</details>

<details><summary> IBM Brand Team </summary>

#### Brand Technical Specialist
* Bill Tice
* Jishnu Desai

#### Brand Sales Specialist
* Pete Ingrasci

#### Account Technical Leader
* Effron Esseiva
  
</details>
