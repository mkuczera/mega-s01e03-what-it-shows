<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import { groupByCause, uniqueById, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  let { parserIssue, hintIssue }: { parserIssue?: string; hintIssue?: string } = $props();

  const merged = uniqueById(reports as Report[]).filter((report) => report.mergedInto === 4471);
  const groups = groupByCause(merged, tenantOf);
  const issueFor = (cause: string) => cause === 'parser' ? parserIssue : cause === 'hint' ? hintIssue : undefined;
</script>

<p><strong>{merged.length}</strong> distinct reports merged into #4471; <strong>{groups.length}</strong> causes.</p>

<table>
  <thead><tr><th>Cause</th><th>Reports</th><th>Tenants</th><th>First seen</th><th>Last seen</th><th>Issue</th></tr></thead>
  <tbody>
    {#each groups as group (group.cause)}
      <tr>
        <td><code>{group.cause}</code></td>
        <td>{group.reports.length}</td>
        <td>{group.tenants}</td>
        <td>{group.firstSeen}</td>
        <td>{group.lastSeen}</td>
        <td>{#if issueFor(group.cause)}<a href={issueFor(group.cause)}>{group.cause} issue</a>{:else}pending{/if}</td>
      </tr>
    {/each}
  </tbody>
</table>

<p>Counts use report IDs, since export pages can overlap. Intake tags are guesses; the cause uses each tenant's locale and booking form.</p>
