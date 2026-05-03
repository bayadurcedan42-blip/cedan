# cedan
foto-utguması
import React, { useState } from "react";
import { View, Text, Button, Image, FlatList } from "react-native";
import * as ImagePicker from "expo-image-picker";

export default function App() {
  const [photos, setPhotos] = useState([]);

  const takePhoto = async () => {
    let result = await ImagePicker.launchCameraAsync({
      allowsEditing: true,
      quality: 0.5,
    });

    if (!result.canceled) {
      setPhotos([...photos, result.assets[0].uri]);
    }
  };

  return (
    <View style={{ marginTop: 50, padding: 20 }}>
      <Text style={{ fontSize: 20, marginBottom: 20 }}>
        📸 Görev: Market rafı fotoğrafı çek
      </Text>

      <Button title="Fotoğraf Çek" onPress={takePhoto} />

      <FlatList
        data={photos}
        renderItem={({ item }) => (
          <Image
            source={{ uri: item }}
            style={{ width: 200, height: 200, marginTop: 10 }}
          />
        )}
        keyExtractor={(item, index) => index.toString()}
      />
    </View>
  );
}
