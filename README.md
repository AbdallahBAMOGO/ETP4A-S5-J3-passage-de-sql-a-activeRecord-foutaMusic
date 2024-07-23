# ETP4A-S5-J3-passage-de-sql-a-activeRecord-foutaMusic
Plus de requête sql

### a) Niveau facile
# Quel est le nombre total d'objets Album contenus dans la base ?
Album.count

# Qui est l'auteur de la chanson "White Room" ?
Track.find_by(title: "White Room").artist

# Quelle chanson dure exactement 188133 milliseconds ?
Track.find_by(duration: 188133).title

# Quel groupe a sorti l'album "Use Your Illusion II" ?
Album.find_by(title: "Use Your Illusion II").artist


### b) Niveau Moyen
# Combien y a t'il d'albums dont le titre contient "Great" ?
Album.where("title LIKE ?", "%Great%").count

# Supprime tous les albums dont le nom contient "music".
Album.where("title LIKE ?", "%music%").destroy_all

# Combien y a t'il d'albums écrits par AC/DC ?
Album.where(artist: "AC/DC").count

# Combien de chansons durent exactement 158589 millisecondes ?
Track.where(duration: 158589).count


### c) Niveau Difficile
# puts en console tous les titres de AC/DC.
acdc_tracks = Track.where(artist: "AC/DC")
acdc_tracks.each { |track| puts track.title }

# puts en console tous les titres de l'album "Let There Be Rock".
let_there_be_rock_tracks = Track.where(album: "Let There Be Rock")
let_there_be_rock_tracks.each { |track| puts track.title }

# Calcule le prix total de cet album ainsi que sa durée totale.
total_price = let_there_be_rock_tracks.sum(:price)
total_duration = let_there_be_rock_tracks.sum(:duration)
puts "Prix total: #{total_price}, Durée totale: #{total_duration} ms"

# Calcule le coût de l'intégralité de la discographie de "Deep Purple".
deep_purple_tracks = Track.where(artist: "Deep Purple")
total_cost = deep_purple_tracks.sum(:price)
puts "Coût total de la discographie de Deep Purple: #{total_cost}"

# Modifie (via une boucle) tous les titres de "Eric Clapton" afin qu'ils soient affichés avec "Britney Spears" en artist.
eric_clapton_tracks = Track.where(artist: "Eric Clapton")
eric_clapton_tracks.each do |track|
  track.update(artist: "Britney Spears")
end
