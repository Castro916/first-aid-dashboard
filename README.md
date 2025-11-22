import React from "react";
import { View, Text, StyleSheet, TouchableOpacity, Alert } from "react-native";
import Icon from "react-native-vector-icons/FontAwesome"; // You'd need to install this library

// Dummy data for saved contacts and general emergency numbers
const EMERGENCY_CONTACTS = [
  { id: "1", name: "Family Contact 1", number: "555-1234" },
  { id: "2", name: "Family Contact 2", number: "555-5678" },
];

const EMERGENCY_SERVICES = [
  { id: "police", name: "Police", number: "999", icon: "shield" },
  { id: "ambulance", name: "Ambulance", number: "999", icon: "ambulance" },
  { id: "fire", name: "Fire", number: "999", icon: "fire" },
];

// Function to simulate a phone call (actual implementation requires device-specific APIs like Linking)
const initiateCall = (number, contactName) => {
  // In a real app, you'd use Linking.openURL(`tel:${number}`)
  Alert.alert(`Calling ${contactName}`, `Attempting to dial: ${number}`);
};

const DashboardScreen = ({ navigation }) => {
  const handleSOSPress = () => {
    // Logic for a global SOS button:
    // 1. Get user's current location (requires geolocation permission)
    // 2. Call local emergency service (e.g., 911 or a single default contact)
    // 3. Send SMS/notification to all EMERGENCY_CONTACTS with location details
    Alert.alert(
      "SOS Triggered!",
      "Location shared and emergency services/contacts notified."
    );
  };

  return (
    <View style={styles.container}>
      {/* 🛑 Main SOS Button Section 🛑 */}
      <TouchableOpacity style={styles.sosButton} onPress={handleSOSPress}>
        <Text style={styles.sosText}>🚨 SOS</Text>
        <Text style={styles.sosSubText}>One-Tap Emergency</Text>
      </TouchableOpacity>

      <View style={styles.section}>
        <Text style={styles.sectionTitle}>Quick Emergency Services</Text>
        <View style={styles.serviceButtons}>
          {EMERGENCY_SERVICES.map((service) => (
            <TouchableOpacity
              key={service.id}
              style={styles.serviceButton}
              onPress={() => initiateCall(service.number, service.name)}
            >
              <Icon name={service.icon} size={30} color="#fff" />
              <Text style={styles.serviceText}>{service.name}</Text>
            </TouchableOpacity>
          ))}
        </View>
      </View>

      <View style={styles.section}>
        <Text style={styles.sectionTitle}>My Primary Contacts</Text>
        {EMERGENCY_CONTACTS.map((contact) => (
          <TouchableOpacity
            key={contact.id}
            style={styles.contactItem}
            onPress={() => initiateCall(contact.number, contact.name)}
          >
            <Text style={styles.contactName}>{contact.name}</Text>
            <Text style={styles.contactNumber}>{contact.number}</Text>
          </TouchableOpacity>
        ))}
        {/* Navigation to a full list management screen */}
        <TouchableOpacity
          style={styles.manageButton}
          onPress={() => navigation.navigate("ManageContacts")}
        >
          <Text style={styles.manageText}>Manage All Contacts →</Text>
        </TouchableOpacity>
      </View>

      {/* Navigation to First Aid Content */}
      <TouchableOpacity
        style={styles.guideButton}
        onPress={() => navigation.navigate("FirstAidGuides")}
      >
        <Text style={styles.guideText}>📖 First Aid Guides</Text>
      </TouchableOpacity>
    </View>
  );
};

// --- Stylesheet ---
const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: "#f5f5f5",
  },
  sosButton: {
    backgroundColor: "#dc3545", // Red color
    padding: 25,
    borderRadius: 15,
    alignItems: "center",
    marginBottom: 20,
    elevation: 5, // Shadow for Android
    shadowColor: "#000", // Shadow for iOS
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.25,
    shadowRadius: 3.84,
  },
  sosText: {
    fontSize: 48,
    fontWeight: "bold",
    color: "#fff",
  },
  sosSubText: {
    fontSize: 14,
    color: "#fff",
    marginTop: 5,
  },
  section: {
    marginBottom: 20,
    backgroundColor: "#fff",
    padding: 15,
    borderRadius: 10,
    elevation: 2,
    shadowOpacity: 0.1,
    shadowRadius: 2,
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: "600",
    marginBottom: 10,
    color: "#333",
  },
  serviceButtons: {
    flexDirection: "row",
    justifyContent: "space-between",
  },
  serviceButton: {
    flex: 1,
    marginHorizontal: 5,
    backgroundColor: "#007bff", // Blue color
    padding: 15,
    borderRadius: 8,
    alignItems: "center",
  },
  serviceText: {
    color: "#fff",
    marginTop: 5,
    fontWeight: "bold",
  },
  contactItem: {
    flexDirection: "row",
    justifyContent: "space-between",
    paddingVertical: 10,
    borderBottomWidth: 1,
    borderBottomColor: "#eee",
    alignItems: "center",
  },
  contactName: {
    fontSize: 16,
    color: "#333",
  },
  contactNumber: {
    fontSize: 16,
    fontWeight: "bold",
    color: "#28a745", // Green color
  },
  manageButton: {
    marginTop: 10,
    alignItems: "flex-end",
  },
  manageText: {
    color: "#007bff",
    fontSize: 14,
  },
  guideButton: {
    backgroundColor: "#ffc107", // Yellow/Orange color
    padding: 15,
    borderRadius: 10,
    alignItems: "center",
    marginTop: 10,
    elevation: 3,
  },
  guideText: {
    fontSize: 18,
    fontWeight: "bold",
    color: "#333",
  },
});

export default DashboardScreen;
