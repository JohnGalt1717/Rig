# Deploy from the repo

The setup of Rig in a repo is code. It is committed. `/init` reads it. A later change is a diff.

That same config generates the pipeline. A check-in that changes a resource, a setting, or a migration emits the deploy step: spin the resource, apply the migration, run the tests, tear down what the diff removed. The pipeline is generated. It is not a file someone maintains beside the config.

The first targets are the three large clouds. A plugin maps a resource to the managed service. The config does not grow a second copy per cloud.

## Later

Libraries for the major languages let a deploy step be code. A C# project can call the Rig deploy API and extend what gets deployed, to the clouds the plugins already know. That is after the generated pipeline is proven. It is not in the first cut.

The first proof is C# and Flutter. Next.js and Vite follow as packs.
