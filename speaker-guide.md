# Speaker's guide

This is a checklist for the speaker to go through before and during the workshop. Not mandatory but useful. Slides for the intro parts can be found [here](https://docs.google.com/presentation/d/1lkmbcvWCa5fuyJiTATT5dxSPkYDmQT_LMUJUkGlYKE8/edit?usp=sharing)

Points which are labelled INTERACTIVE should be done by workshop participants too. The idea is that they can try out collaboration on live experiments together with the speaker.

## Preparation
- [ ] Create a new GitHub repo from this template (ideally in your personal account so that the number of collaborator seats is not limited)
- [ ] Clean up the [workshop account](https://www.notion.so/iterative/AWS-Workshop-Account-9bd3e98a7f3e43e4af03d367da769ffd) on AWS (remove all Sagemaker endpoints, remove associated S3 buckets wipe clean the DVC remote bucket)
- [ ] Add credentials to the new GH repo (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SAGEMAKER_ROLE)
- [ ] have the AWS credentials set up locally (workshop participants will not need them though)
- [ ] Create a new Studio team (with enough seats, but expiring soon, maybe in a week...or you can delete the team after the workshop)
- [ ] Add the GH repo to Studio as a project
- [ ] Add the AWS credentials to the Studio project 

## Intro and Setup
- [ ] Invite people to GH repo, ideally before the workshop itself (those who missed it can fork and work individually)
- [ ] Intro of Iterative and the speaker:
  - [ ] Briefly mention main areas:
    - [ ] DVCx: large unstructured data / pre-processing (not topic of the talk)
    - [ ] DVC (etc.): GitOps-like MLOps
    - [ ] Studio - a platform for the DVC ecosystem
    - [ ] Mention that a lot can be done just with FOSS but e.g. shared MR for all repos and shared experiments cannot, plus easier to use by less technical users => collaborative aspect
- [ ] Open Repo, brief outline (what project we will be doing today, show final state from a previously forked project in Studio)
- [ ] Invite people to the Studio team (again, this is even better done before the workshop)
- [ ] INTERACTIVE: Set up Studio token
- [ ] INTERACTIVE: Install a virtual environment (this is done now since it will take some time you can use to go through slides)


## Intro
- [ ] ML Lifecycle:
  - [ ] Why should I bother with GitOps?
  - [ ] What we'll do and what we won't have time to do
- [ ] DVC versioning:
  - [ ] .dvc files as "pointers" to data
  - [ ] explain how it all works (UI and a lot of the logic is git-like)
  - [ ] INTERACTIVE: `dvc import` raw data, show `.dvc` file
  - [ ] (yourself) - set up dvc credentials, show people briefly the dvc remote config


## Pipelines
- [ ] show scripts in the pipeline (briefly, do not explain dvclive yet) 
- [ ] show dvc.yaml file, explain stages and how they work with outputs and deps, but not too much detail yet
- [ ] show params file (people will want to edit that when running experiments)

## Experiments
- [ ] INTERACTIVE: change `params.yaml` and run your own experiments with `dvc exp run`
- [ ] observe live tracking and results in Studio
- [ ] Compare metrics and plots in Studio between experiments (from you and participants)
- [ ] Zoom into what happens under the hood:
  - [ ] Show how dvc.yaml changed => how stuff is logged (now go to scripts briefly and show dvclive)
  - [ ] show dvc.lock file => reproducibility! versioning! This is the connection to GitOps - emphasize similarity to .dvc files, but now for entire pipelines
  - [ ] run again to demonstrate what happens if nothing changed (DVC knows the hashes of deps have not changed)
  - [ ] Explain that experiments are git commits tucked away from git history (but visible in Studio for sharing), kind of like git stash

## Model registry
- [ ] Persist your experiment (as a commit to main or with `dvc exp branch`)
- [ ] show model registry in Studio...
- [ ] why is there a model already? Explain that `dvclive.log_artifact()` registers models via dvc.yaml
- [ ] Add model version (maybe two)
- [ ] show connection to experiments (metrics, params ...)
- [ ] Add a stage or two
- [ ] How are the MR actions connected to git? Show connection between MR history and git tags, mention GTO

## Model deployment
- [ ] Show that we have just deployed the model behind the scenes! (show running workflow on GitHub)
- [ ] Show the GA workflow file:
  - [ ] running "on tags"
  - [ ] GTO action parsing events (can be done without the action also) => used as conditions for deployment
  - [ ] Using `dvc get` to obtain model (or URL in Sagemaker case)
- [ ] Demonstrate inference in notebook

## End

- [ ] Recap what we did, how every part is connected to GitOps
- [ ] If there is time, mention cloud experiments (from Studio, with CML, ...)
