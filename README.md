
# Ubuntu dotnet Act image

🤓 Run your GitHub Actions for **.NET** / **Docker** / **Helm** workflows from your local computer 🖥️🚀!

⚠️ Make sure to read about the environment in which this Docker image runs. Some setup is necessary if you require **secrets**  / **environment variables**. 

⚠️ This image requires to run in privileged mode!

## Environment

There are two main mount points for your attention:

* **/env**

This location is used by the [act tool](https://github.com/nektos/act) to read secrets and environment variables.

* Make sure that your **/env** mount point contains the following files for running GitHub Actions:

	*  **local-build.secrets**
	
		``SECRET_KEY="SECRET VALUE"``
	
	* **local-build.env**
	
		``ENV_KEY="ENV VALUE"``

* **/gh**

This is the entrypoint path for running your GitHub Actions workflows. 

Make sure the **.github** folder is at the root of **/gh** so that [act](https://github.com/nektos/act) can pick it up and run your workflow!
    
## How to use

* ☝️ If you need to use custom NuGet feeds, make sure that you copy your **NuGet.Config** file into the root of the solution where ``dotnet build`` will be invoked. You can create local tooling that temporarily copies your ``~/NuGet.Config`` into your source directory and invoke the image with necessary files already present for mounting to **/gh**.

* ☝️ Any tooling that is able to read config files can be treated similarly to **NuGet.Config**, simply copy the needed files into your solution BEFORE mounting the volumes for **dotnet-ubuntu-act**.

### Running

````bash
docker run -v YOUR_PATH_TO_SECRETSANDENV:/env \
-v YOUR_PATH_TO_PROJECT:/gh \
--privileged \
karolczajkowski/dotnet-ubuntu-act
````

Will execute your project's workflow located in ``YOUR_PATH_TO_PROJECT``'s ``.github/workflows/`` directory.

## Notable mentions

[Act](https://github.com/nektos/act) is phenomenal. Give them a star of appreciation!

The underlying image to run workflows can be found [here](https://github.com/karolswdev/dotnet-ubuntu-dind).




