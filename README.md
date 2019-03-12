Conda Environment Buildpack
===========================

This is the [Heroku Buildpack][] for [Conda][] using it's new
[environment spec][].  Anything you can install with `conda install` can be
installed using this in the post_containerize script.

## Usage
To control what gets installed, create an `environment.yml` file in the root
of your repository.  For example, if you wanted to install Flask, you would add
this:

```yaml
name: myproject  # overridden at install, so this is for your use with conda env
dependencies:
  - flask
```

To run a server on your ship create a `Procfile` that is one line and looks like:

```bash
web: source activate /home/ubuntu/app/.heroku/miniconda/envs/heroku-env; gunicorn server:app --bind 0.0.0.0:$PORT --timeout 90;
```

to use your custom code change only the gunicorn part, the activate has to be done to use the conda env you built from your environment.yml (this buildpack will name it heroku-env)


## Sample Project:
* https://github.com/glg/embedding_search
* https://github.com/glg/ec2.starphleet.dev.headquarters/tree/TristanWise/embedding_search


[Conda]: http://conda.io
[environment spec]: https://github.com/conda/conda-env#environmentyml
[Heroku Buildpack]: https://devcenter.heroku.com/articles/buildpacks

