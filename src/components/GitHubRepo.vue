<template>
    <div>
        <!-- TODO: Crear componente GitHubRepo -->
		<div class="col-12">
			<div class="card my-4">
				<div class="card-header">
					<h5 class="card-title">{{repo.full_name}}</h5>
				</div>
				<div class="card-body">
					<p class="card-text">{{repo.description}}</p>        
					<a type="button" class="btn btn-outline-primary btn-block align-self-center" aria-pressed="true" :href="repo.html_url" target="_blank" >ver</a>
				</div>
				<div class="card-footer text-right"> 
					<span class="badge badge-pill badge-danger">{{repo.open_issues_count}} Issues</span>
				</div>
			</div>
		</div>
		
    </div>
</template>

<script>
export default {
    name: 'GitHubRepo',
    props: [
        // TODO: crear parámetro 'repo'
		"repo"
    ],
}
</script>

<style scoped>
</style>
