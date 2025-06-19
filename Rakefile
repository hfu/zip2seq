ISO3S = ["tls", "pan", "vut", "tha", "mmr", "ken", "dji", "sen", "jor"]
THEME = "education_facilities"
GEOMS = ["polygons", "points"]

S3_URL_BASE = "https://s3.dualstack.us-east-1.amazonaws.com/production-raw-data-api/ISO3/"

desc "各ISO3ごとに複数GEOMのGeoJSONSeqを連結し、tippecanoeでPMTilesとGeoJSONを作成"
task :tippecanoe do
  ISO3S.each do |iso3|
    output_pmtiles = "docs/#{iso3}_#{THEME}.pmtiles"
    output_geojson = "docs/#{iso3}_#{THEME}.geojson"
    puts "Creating PMTiles: #{output_pmtiles}"
    puts "Creating GeoJSON: #{output_geojson}"

    geojsonseq_cmds = GEOMS.map do |geom|
      s3_url = "#{S3_URL_BASE}#{iso3.upcase}/#{THEME}/#{geom}/hotosm_#{iso3}_#{THEME}_#{geom}_geojson.zip"
      entry  = "hotosm_#{iso3}_#{THEME}_#{geom}_geojson.geojson"
      layer  = "#{iso3}_#{THEME}_#{geom}"
      "curl -L #{s3_url} | bsdtar -xOf - #{entry} | jq -c '.features[] | .tippecanoe = { layer: \"#{layer}\" }'"
    end

    system("bash", "-c", "( #{geojsonseq_cmds.join(' ; ')} ) | tee >(tippecanoe -o #{output_pmtiles} --force) | ogr2ogr -f GeoJSON #{output_geojson} /vsistdin/")
  end
end

task :default => :tippecanoe
