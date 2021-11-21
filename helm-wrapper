#! /bin/sh

# helm.bin is the original helm binary
case $1 in
  show*)
    exec /usr/local/bin/helm.bin $@
    ;;
  template*)
    # when running 'helm template . ', if it detects "secrets.yaml", helm-secrets will try to decrypt it.
    # After decryption, sops will automatically generate "secrets.yaml.enc".
    # the helm-secret plugs inherit sops' behavour.
    # This grep workaround the situation, remove the last line.
    # Otherwise, ArgoCD will fail to parse the mal-formed yaml.
    exec /usr/local/bin/helm.bin secrets $@ | grep -ve '^removed .*$'
    ;;
  *)
    exec /usr/local/bin/helm.bin secrets $@
    ;;
esac
