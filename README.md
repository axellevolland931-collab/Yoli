// mobile_app/lib/providers/user_profile_provider.dart
import 'package:flutter_riverpod/flutter_riverpod.dart';
import '../models/concert_model.dart';

// Имитация данных профиля
final initialProfile = UserProfile(
  userId: 'U-001',
  preferredGenres: ['Rock', 'Indie', 'Alternative'],
  followingArtistIds: ['A-101', 'A-205'],

final userProfileProvider = StateNotifierProvider<UserProfileNotifier, UserProfile>((ref) {
  return UserProfileNotifier(initialProfile);
});

class UserProfileNotifier extends StateNotifier<UserProfile> {
  UserProfileNotifier(UserProfile initialProfile) : super(initialProfile);
  
  void followArtist(String artistId) {
    if (!state.followingArtistIds.contains(artistId)) {
      state = UserProfile(
        userId: state.userId,
        preferredGenres: state.preferredGenres,
        followingArtistIds: [...state.followingArtistIds, artistId],
      )
  
  void unfollowArtist(String artistId) {
    state = UserProfile(
      userId: state.userId,
      preferredGenres: state.preferredGenres,
      followingArtistIds: state.followingArtistIds.where((id) => id != artistId).toList(),
    );
    print('PROFILE: Отписка от артиста $artistId оформлена.');
  }
}
