---
layout: default
title:  Getting Started with <span class="notransform">GoCD</span> - Part 1
title_tag: Getting Started | GoCD
meta_tag_description: New to GoCD? Start here.
meta_tag_keywords: getting started, documentation, gocd, continuous delivery, go
page_name: getting-started page-1
extra_headers: "<link rel='stylesheet' href='/css/getting-started.css'>"
---

Welcome to GoCD! In this guide, you'll learn about some of GoCD's concepts and features, and get the chance to try them out on a real server.

##### Table of contents:

- [Installation](#installation)
  - [Concept 1: Server and agents](#concept_server_and_agents)
- [Creating a pipeline](#creating_pipeline)
   - [Concept 2: Pipelines and materials](#concept_pipelines_and_materials)
   - [Concept 3: Agent prepares to do some work](#concept_agent_does_work)
   - [Concept 4: Stages, jobs and tasks](#concept_stages_jobs_tasks)
- [Next part of guide (different page): Part 2](/getting-started/part-2.html)
- [Next part of guide (different page): Part 3](/getting-started/part-3.html)

<h2 class="small_margins"><a name="installation"></a>Installation</h2>

If you haven't installed GoCD yet, you can follow the
[GoCD Installation Guide](https://www.go.cd/documentation/user/current/installation/index.html) to install the GoCD
Server at least one GoCD Agent. This is a good point to stop and learn about the first concept in GoCD.

<div class="concept">
  <h3><a name="concept_server_and_agents"></a>Concept 1: Server and agents</h3>

  <figure class="concept">
    <img src="/images/getting-started/part-1/image01.png">
  </figure>

  <p>
    In the GoCD ecosystem, the server is the one that controls everything. It provides the user interface to users of the
    system and provides work for the agents to do. The agents are the ones that do any work (run commands, do deployments,
    etc) that is configured by the users or administrators of the system.
  </p>

  <p>
    The server does not do any user-specified "work" on its own. It will not run any commands or do
    deployments. That is the reason you need a GoCD Server and at least one GoCD Agent installed before you proceed.
  </p>
</div>

Once you have them installed and running, you should see a screen similar to this, if you navigate to the home page in
a web browser (defaults to: [http://localhost:8153](http://localhost:8153)):

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image02.png">
  <figcaption>GoCD's new pipeline page</figcaption>
</figure>

If you have installed the GoCD Agent properly and click on the "Agents" link in the header, you should
see an idle GoCD agent waiting (as shown below). If you do not, head over to the
[troubleshooting page](/documentation/user/current/installation/troubleshoot_installer.html) to figure out why.

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image03.png">
  <figcaption>Agents page</figcaption>
</figure>

Congratulations! You're on your way to using GoCD. If you now click "Pipelines", you'll get back
to the "Add pipeline" screen you saw earlier.

<h2 class="small_margins"><a name="creating_pipeline"></a>Creating a pipeline</h2>

Before creating a pipeline, it might help to know what it is and concepts around it.

<div class="concept">
  <h3><a name="concept_pipelines_and_materials"></a>Concept 2: Pipelines and materials</h3>

  <figure class="concept">
    <img src="/images/getting-started/part-1/image04.png">
    <figcaption></figcaption>
  </figure>

  <p>
    A pipeline, in GoCD, is a representation of workflow or a part of a workflow. For instance, if you are trying to
    automatically run tests, build an installer and then deploy an application to a test environment, then those steps can
    be modeled as a pipeline. GoCD provides different modeling constructs within a pipeline, such as stages, jobs and
    tasks. We will see these in more detail soon. For the purpose of this part of the guide, you need to know that a
    pipeline can be configured to run a command or set of commands.
  </p>

  <p>
    Another equally important concept is that of a material. A material is a cause for a pipeline to "trigger"
    or to start doing what it is configured to do. Typically, a material is a source control repository (like Git,
    Subversion, etc) and any new commit to the repository is a cause for the pipeline to trigger. A pipeline needs to
    have at least one material and can have as many materials of different kinds as you want.
  </p>

  <p>
    The concept of a pipeline is extemely central to Continuous Delivery. Together with the concepts of stages, jobs and
    tasks, GoCD provides important modeling blocks which allow you to build up very complex workflows, and get feedback
    quicker. You'll learn more about GoCD pipelines and Deployment pipelines in the upcoming parts of this guide. In
    case you cannot wait, Martin Fowler has a nice and succint article <a
    href="http://martinfowler.com/bliki/DeploymentPipeline.html">here</a>.
  </p>
</div>

Now, back at the "Add pipeline" screen, let's provide the pipeline a name, without spaces, and ignore
the "Pipeline Group" field for now.

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image05.png">
  <figcaption>Step 1: Name your pipeline</figcaption>
</figure>

Pressing "Next" will take you to step 2, which can be used to configure a material.

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image06.png">
  <figcaption>Step 2a: Point it to a material - Where to look for changes?</figcaption>
</figure>

You can choose your own material here <sup><a href="#fn1" id="r1">[1]</a></sup>, or use a Git repository available on
GitHub for this guide. The URL of that repository is: <span class="nobreak"><a
href="https://github.com/gocd-contrib/getting-started-repo.git">https://github.com/gocd-contrib/getting-started-repo.git</a></span>. You
can change "Material Type" to "Git" and provide the URL in the "URL" textbox. If you now click on the "Check Connection"
button, it should tell you everything is OK.

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image07.png">
  <figcaption>Step 2b: Check that the material exists</figcaption>
</figure>

This step assumes that you have git installed on the GoCD Server and Agent. Like git, any other commands you need for
running your scripts need to be installed on the GoCD Agent nodes.

If you had trouble with this step, and it failed, take a look at the
[troubleshooting page](/documentation/user/current/installation/troubleshoot_installer.html) in the documentation. If
everything went well, press "Next" to be taken to step 3, which deals with stages, jobs and tasks.

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image08.png">
  <figcaption>Step 3a: Use the predefined stage and job for now</figcaption>
</figure>

Since a stage name and a job name are populated, and in the interest of quickly achieving our goal of creating and
running a pipeline in GoCD, let us delay understanding the (admittedly very important) concepts of stage and job and
focus on a task instead. Scrolling down a bit, you'll see the "Initial Job and Task" section.

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image09.png">
  <figcaption>Step 3b: Take a closer look at the initial job and task</figcaption>
</figure>

Since we don't want to use "Ant" right now, let's change the "Task Type" to "More...". You should see a screen like this:

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image10.png">
  <figcaption>Step 3c: Choose a custom command</figcaption>
</figure>

Change the text of the "Command" text box to "./build" (that is, dot forward-slash build) and press "Finish". If all
went well, you just created your first pipeline! Leaving you in a screen similar to the one shown below.

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image11.png">
  <figcaption>Your first pipeline (paused)</figcaption>
</figure>

Helpfully, the pipeline has been paused for you (see the pause button and the text next to it, right next to the
pipeline name). This allows you to make more changes to the pipeline before it triggers. Usually, pipeline
administrators can take this opportunity to add more stages, jobs, etc. and model their pipelines better. For the
purpose of this guide, let's just un-pause this pipeline and get it to run. Click on the blue "pause" button and then
click on the "Pipelines" link in the header.

If you give it a minute, you'll see your pipeline building (yellow) and then finish successfully (green):

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image12.png">
  <figcaption>The pipeline is building</figcaption>
</figure>

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image13.png">
  <figcaption>The pipeline finished successfully</figcaption>
</figure>

Clicking on the bright green bar will show you information about the stage:

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image14.png">
  <figcaption>Information about the stage</figcaption>
</figure>

and then clicking on the job will take you to the actual task and show you what it did:

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image15.png">
  <figcaption>The output of the job run</figcaption>
</figure>

Scrolling up a bit, you can see it print out the environment variables for the task and the details of the agent this
task ran on (remember "Concept 1"?).

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image16.png">
  <figcaption>The environment variables used for the job</figcaption>
</figure>

<figure class="screenshot">
  <img src="/images/getting-started/part-1/image17.png">
  <figcaption>Job run details</figcaption>
</figure>

<div class="concept">
  <h3><a name="concept_agent_does_work"></a>Concept 3: Agent prepares to do some work</h3>

  <p>
    Did you notice the lines at the top of the build which said: "Start updating files at revision ..."? This is the agent
    preparing to run the job configured. Every material configured for that pipeline will be updated to the correct
    revision, so that it is consistent with the rest of the pipeline and the system as a whole.
  </p>

  <p>
    Once the material is checked out (if it is the first time it is ever used) and updated to the correct revision, it will
    be available for use in a task. That is the reason the build script, "./build" was available without you having to do
    anything. It is found inside the configured <a
    href="https://github.com/gocd-contrib/getting-started-repo/blob/ea5d1406aa6408c2fb920965d1c0e3e8564db14f/build">Git
    repository material</a>.
  </p>

  <p>
    In this case, we had only one material, and so we could use it as "./build". If you had configured more materials, you'd
    need to provide a working directory for each material and would have had to use the script as "./material1/build" (for
    instance).
  </p>

  <p>
    Notice that the GoCD Agent independently checks out the repository, meaning that the version control systems of your
    materials (Git, SVN, etc) need to be available on the GoCD Agent as well.
  </p>
</div>


Now that you have a basic idea of a pipeline and what it does, let's understand more about its components.

<div class="concept">
  <h3><a name="concept_stages_jobs_tasks"></a>Concept 4: Stages, jobs and tasks</h3>

  <figure class="concept">
    <img src="/images/getting-started/part-1/image18.png">
    <figcaption></figcaption>
  </figure>

  <p>
    A pipeline consists of one or more "stages", each stage consists of one or more "jobs" and each job is made up of one or
    more "tasks". All of these are modeling constructs within a pipeline. Starting from the smallest piece:
  </p>

  <dl>
    <dt>Task</dt>
    <dd>
      A task is typically a command which is configured to run as a part of the job it is in. Not every task needs to be
      a simple command, since tasks can be plugins. In this guide, the "./build" that was configured to run was a task. GoCD has
      Ant, NAnt and Rake tasks as built-in tasks, but has many more optional plugins which can be installed. The most
      versatile built-in task is the one that was used in this guide, which is the "Custom Command". Whenever anyone asks the
      question, "Can GoCD run &lt;application-x&gt;?, the answer is always "Yes", because it can always be executed as a custom
      command.
    </dd>
  </dl>

  <dl>
    <dt>Job</dt>
    <dd>
      A job is a sequential collection of tasks. Each task in a job is run one after the other, and in its default
      configuration, if a task fails, none of the tasks following that one get executed. The job is then considered to have
      "failed". The most important aspect of a job is that a <em>single</em> agent has to pick up and finish a job. So, you can be
      guaranteed that all tasks in a job run on the <em>same</em> agent.
    </dd>
  </dl>

  <dl>
    <dt>Stage</dt>
    <dd>
      A stage is a collection of jobs, but the jobs are not sequential. They can be picked up in any order and so, they
      have to be <em>independent</em> of each other. This crucial distinction between how a job is composed of its tasks (sequential)
      and how a stage is composed of its jobs (non-sequential) is what provides built-in parallelizability in GoCD. Since jobs
      in a stage are independent of each other, they will all be started together, when a stage starts. Assuming that you have
      enough agents started and not busy, then every job in a stage can run on a different agent at the same time, potentially
      speeding up your build by a lot.
    </dd>
  </dl>

  <p>
    Circling back to the pipeline we created in this guide: The pipeline had one stage called "defaultStage" and one job in
    that stage called "defaultJob" and had only one task in that - a custom command task, which ran: "./build".
  </p>
</div>

This is just the tip of the iceberg in terms of GoCD's features and capabilities. In the upcoming parts of this guide,
you will learn more about some more of GoCD's core features, such as fan-in, fan-out, artifact promotion, pipeline
dependencies, value stream maps and more.

Let's start, in [Part 2](/getting-started/part-2.html) of this guide, where you can learn about pipeline dependencies and artifacts.

#### Notes:

<section>
  <p id="fn1">
    <a href="#r1">[1]</a>
    If you're used to using Git or any version control system used by GoCD, you can clone your repository locally and
    provide that path instead of using the repository on GitHub used in this guide. That way, you can make commits to
    your repository and see pipelines triggering because of them.
  </p>
</section>
