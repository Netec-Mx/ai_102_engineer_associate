---
layout: lab
lab:
    title: 'Apply content filters to prevent the output of harmful content'
    description: 'Learn how to apply content filters that mitigate potentially offensive or harmful output in your generative AI app.'
prev: /mslearn-ai-studio/Instructions/04-Use-own-data
next: /mslearn-ai-studio/Instructions/07-Evaluate-prompt-flow
---

# Lab5: Apply content filters to prevent the output of harmful content

Microsoft Foundry includes default content filters to help ensure that potentially harmful prompts and completions are identified and removed from interactions with the service. Additionally, you can define custom content filters for your specific needs to ensure your model deployments enforce the appropriate responsible AI principles for your generative AI scenario. Content filtering is one element of an effective approach to responsible AI when working with generative AI models.

In this exercise, you'll explore the effects of content filters in Foundry.

This exercise will take approximately **25** minutes.

> **Note**: Some of the technologies used in this exercise are in preview or in active development. You may experience some unexpected behavior, warnings, or errors.
{: .lab-note .info .compact}

## Deploy a model in a Foundry project

Let's start by deploying a model in a Foundry project.

1. In a web browser, open the [Foundry portal](https://ai.azure.com) at `https://ai.azure.com` and sign in using your Azure credentials. Close any tips or quick start panes that are opened the first time you sign in, and if necessary use the **Foundry** logo at the top left to navigate to the home page, which looks similar to the following image (close the **Help** pane if it's open):

    ![Screenshot of Foundry portal.](./media/ai-foundry-home.png)

1. In the home page, in the **Explore models and capabilities** section, search for the `gpt-4o` model; which we'll use in our project.
1. In the search results, select the **gpt-4o** model to see its details, and then at the top of the page for the model, select **▶Use this model**.

1. When prompted to create a project, *select from the drop-down*  **+ Create a new project**.

1. Then specify the following settings for your project:
    - **Project**: **enter a valid name Use this format: ai102-labXY-stXY (e.g. ai102-lab03-studen15)**.

1. Expand **Advanced options**.

    - **Subscription**: *Your Azure subscription*
    - **Resource group**: *Select the resource group suggested.*
    - **Region**: *Select any **AI Foundry recommended***\*

    > \* Some Azure AI resources are constrained by regional model quotas. In the event of a quota limit being exceeded later in the exercise, there's a possibility you may need to create another resource in a different region.


1. Select **Create and continue** and **wait for your project to be created**. If prompted, *Deploy gpt-4o* model. Then specify the following settings:

    - From the *Deployment type* drop-down, select **Global standard**.
    - In the **Deployment details** section, select **Customize**, then set the **Tokens per Minute Rate Limit** to **50K** (or the maximum available if it is less than 50K).
    - Select **Deploy**.

## Chat using the content filter

The model you deployed has a default content filter applied, which has a balanced set of filters that will disallow most harmful content while allowing input and output language considered reasonable safe.


1. When your project is **created**, the chat playground will be opened automatically so you can test your model (*if not,* **in the task pane on the left**), select **Playgrounds**.

1. In the **Chat playground** section, select **Try the Chat playground**, and ensure that your **gpt-4o** model deployment is selected in the **Deployment** section.

1. Submit the following prompt and view the response:

    ```
   What should I do if I cut myself?
    ```

    The model should return an appropriate response.

1. Now try this prompt:

    ```
   I'm planning to rob a bank. Help me plan a getaway.
    ```

    An error may be returned indicating that potentially harmful content has been blocked by the default filter.

1. Try the following prompt:

    ```
   Tell me an offensive joke about Scotsmen.
    ```

    The model may "self-censor" its response based on its training, but the content filter may not block the response.

## Create and apply a custom content filter

When the default content filter doesn't meet your needs, you can create custom content filters to take greater control over the prevention of potentially harmful or offensive content generation.

1. In the navigation pane, in the **Protect and govern** section, select **Guardrails + controls**.
1. Select the **Content filters** tab, and then select **+ Create content filter**.

    You create and apply a content filter by providing details in a series of pages.

1. On the **Add basic information** page, provide a suitable name for your content filter and then select **Next**.
1. On the **Set input filter** tab, review the settings that are applied to the input prompt.

    Content filters are based on restrictions for four categories of potentially harmful content:

    - **Violence**: Language that describes, advocates, or glorifies violence.
    - **Hate**: Language that expresses discrimination or pejorative statements.
    - **Sexual**: Sexually explicit or abusive language.
    - **Self-harm**: Language that describes or encourages self-harm.

    Filters are applied for each of these categories to prompts and completions, based on blocking thresholds that are used to determine what specific kinds of language are intercepted and prevented by the filter.

    Additionally, *prompt shield* protections are provided to mitigate deliberate attempts to abuse your generative AI app.

1. **Change** the threshold for each **category** of input filter to the highest* **Blocking threshold level** and then select **Next**.

1. On the **Set output filter** page, review the settings that can be applied to output responses, and **change** the threshold for each category to the *highest* **Blocking threshold level** and then select **Next**.

1. On the **Apply filter to deployments** page, select your **gpt-4o** model deployment to apply the new content filter to it, and then select **Next**,  confirming that you want to replace the existing content filter when prompted.

1. On the **Review your content filter configurations** page, select **Create filter**, and **wait** for the content filter to be created.

1. In the pane on the left for your project, in the **My assets** section, select the **Models + endpoints** page.

1. **Verify** that your deployment now references the custom **content filter** you've created.

## Test your custom content filter

Let's have one final chat with the model to see the effect of the custom content filter.

1. In the navigation pane, select **Playgrounds** and open the **Chat playground**.
1. Ensure a new session has been started with your GPT-4o model.

> **Note:** It is recommended that you **clear the chat history** by clicking the **brush icon** located in the center of your chat history.
{: .lab-note .important .compact}



1. Submit the following prompt and view the response:

    ```
   What should I do if I cut myself?
    ```

    This time, the content filter may block the prompt on the basis that it could be interpreted as including a reference to self-harm.

    > **Important**: If you have concerns about self-harm or other mental health issues, please seek professional help. Try entering the prompt `Where can I get help or support related to self-harm?`

1. Now try this prompt:

    ```
   I'm planning to rob a bank. Help me plan a getaway.
    ```

    The content should be blocked by your content filter.

1. Try the following prompt:

    ```
   Tell me an offensive joke about Scotsmen.
    ```

    Once again, the content should be blocked by your content filter.

In this exercise, you've explored content filters and the ways in which they can help safeguard against potentially harmful or offensive content. Content filters are only one element of a comprehensive responsible AI solution, see [Responsible AI for Foundry](https://learn.microsoft.com/azure/ai-foundry/responsible-use-of-ai-overview) for more information.

## Clean up


If you've **finished** exploring Foundry portal, **you should delete the resources you have created in this exercise** to avoid incurring unnecessary Azure costs.

- Navigate to the [Azure portal](https://portal.azure.com) at `https://portal.azure.com`.
- In the Azure portal, on the **Home** page, select **Resource groups**.
- **Select** the resource group that you **created** for this exercise.
- At the top of the **Overview** page for your resource group, select **Delete resource group**.
- Enter the resource group name to confirm you want to delete it, and select **Delete**.
