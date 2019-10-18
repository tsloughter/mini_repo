allow_k8s_contexts('microk8s')
default_registry("localhost:32000")

custom_build(
    'mini_repo',
    'docker build --target build --tag $EXPECTED_REF .',
    ['.'],
    live_update=[
        sync('lib', '/app/lib'),
        run('mix do compile, release'),
        run('/app/_build/prod/rel/mini_repo/bin/mini_repo restart')
    ],
    entrypoint="/app/_build/prod/rel/mini_repo/bin/mini_repo start",
    ignore=['deployment']
)

k8s_yaml(kustomize('deployment/overlays/dev'))

watch_file('deployment/')
