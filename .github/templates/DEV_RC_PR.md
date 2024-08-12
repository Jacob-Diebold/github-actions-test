# develop -> {{.baseBranchName}}

## Summary

### Changes
{{- $changes := split .existingChanges "|" -}}
{{- range $index, $change := $changes -}}
- {{ $change }}
{{- end -}}