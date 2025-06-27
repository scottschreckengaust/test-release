# README

release/2025.6.20250626211742

```
      - uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2
      - name: Create release
        env:
          GH_TOKEN: ${{ secrets.PAT_TOKEN}}
        run: |
          VERSION="${{ github.run_number }}"
          gh release create "$VERSION" \
            --generate-notes \
            --draft \
            --verify-tag
          echo "# $VERSION" > RELEASE_NOTES.md
          gh release view "$VERSION" --json body | jq -r '.body' > GENERATED_NOTES.md
          cat RELEASE_NOTES.md GENERATED_NOTES.md | gh release edit "$VERSION" \
            --draft=false \
            --notes-file -
```


```
      - name: Debug
        run: |
          echo "::group::GITHUB object"
          echo "${{ toJson(github) }}"
          echo "::endgroup::"
```
